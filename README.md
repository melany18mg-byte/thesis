import pandas as pd
import re

# =========================
# LOAD
# =========================
df = pd.read_excel("c:/Thesis/DATASET_FINALE.xlsx")

# =========================
# CLEAN
# =========================
def clean(x):
    if pd.isna(x):
        return ""
    x = str(x).strip().lower()
    x = re.sub(r"\s+", " ", x)
    return x

df["mol_clean"] = df["molecule_adj_name"].apply(clean)
df["frm_clean"] = df["frm2"].apply(clean)

# =========================
# FILTRO DATI VALIDI
# =========================
invalid_values = {"", "unknown", "nessun principio attivo"}

df = df[
    (~df["mol_clean"].isin(invalid_values)) &
    (~df["frm_clean"].isin(invalid_values))
].copy()

# =========================
# MARKET ID
# =========================
df["market_id"] = df["mol_clean"] + " | " + df["frm_clean"]

company_col = "manufacturer"
product_col = "Product"
atc4_col= "atc4"

# =========================
# COLONNE MENSILI
# =========================
eur_cols = [
    c for c in df.columns
    if c.startswith("sellin_eur_") and re.fullmatch(r"sellin_eur_\d{4}-\d{2}", c)
]

df[eur_cols] = df[eur_cols].fillna(0)

# =========================
# LONG
# =========================
df_long = df.melt(
    id_vars=["atc4_col",
        "market_id",
        company_col,
        product_col,
        "business_rule",   
        "Pack"             
    ],
    value_vars=eur_cols,
    var_name="month",
    value_name="sales"
)

df_long["month"] = df_long["month"].str.replace("sellin_eur_", "", regex=False)

# =========================
# MARKET TOTAL
# =========================
df_long["market_total"] = df_long.groupby(
    ["market_id", "month"]
)["sales"].transform("sum")

# =========================
# PRODUCT SHARE
# =========================
df_long["product_share"] = (
    df_long["sales"] / df_long["market_total"].replace(0, pd.NA)
)

# =========================
# WIDE
# =========================
df_wide = df_long.pivot_table(
    index=["atc4_col",
        "market_id",
        company_col,
        product_col,
        "business_rule",   
        "Pack"             
    ],
    columns="month",
    values="product_share"
)

# =========================
# NOMI COLONNE
# =========================
df_wide.columns = [f"product_share_{m}" for m in df_wide.columns]

df_wide = df_wide.reset_index()

# =========================
# SAVE
# =========================
df_wide.to_csv("c:/Thesis/product_share_wide.csv", index=False)

print("✅ Done")
