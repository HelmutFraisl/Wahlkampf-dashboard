import streamlit as st
import pandas as pd
import plotly.express as px

st.set_page_config(page_title="Wahlkampf-Dashboard Thomas Streber", layout="wide")

st.title("📊 Wahlkampf-Dashboard: Analyse Digihausen")
st.markdown("Optimale Vorbereitung für Thomas Streber basierend auf aktuellen Umfragedaten.")

# File Uploader
uploaded_file = st.file_uploader("Lade die Umfrage-Rohdaten (CSV) hoch", type="csv")

if uploaded_file is not None:
    df = pd.read_csv(uploaded_file)
    
    # Metriken
    col1, col2, col3, col4 = st.columns(4)
    col1.metric("Befragte gesamt", len(df))
    col2.metric("Ø Sympathie Thomas", round(df['Sympathie_Thomas_Streber_1bis5'].mean(), 2))
    col3.metric("Gegen Schulschließung", f"{round((df['Meinung_Schulschliessung'] == 'Dagegen').mean() * 100)}%")
    col4.metric("Top-Leerstand", df['Prioritaet_Leerstand'].mode()[0])

    # Grafiken
    st.divider()
    c1, c2 = st.columns(2)

    with c1:
        st.subheader("Sympathie nach Altersgruppe")
        fig1 = px.bar(df.groupby('Altersgruppe')['Sympathie_Thomas_Streber_1bis5'].mean().reset_index(), 
                      x='Altersgruppe', y='Sympathie_Thomas_Streber_1bis5', color='Altersgruppe', range_y=[0,5])
        st.plotly_chart(fig1, use_container_width=True)

    with c2:
        st.subheader("Meinung zur Schulschließung")
        fig2 = px.pie(df, names='Meinung_Schulschliessung', color_discrete_sequence=px.colors.qualitative.Pastel)
        st.plotly_chart(fig2, use_container_width=True)

    # KI Interpretation
    st.divider()
    st.subheader("🤖 KI-Analyse: Chancen & Risiken")
    
    if df['Sympathie_Thomas_Streber_1bis5'].mean() < 3.5:
        st.warning("**Risiko:** Deine Sympathiewerte sind im neutralen Bereich. Besonders bei jungen Wählern (18-35) musst du präsenter werden.")
    
    if (df['Meinung_Schulschliessung'] == 'Dagegen').sum() > len(df)/2:
        st.error("**Kritisches Risiko:** Eine große Mehrheit ist gegen die Schulschließung. Positioniere dich klar für den Erhalt!")
    
    st.success(f"**Chance:** Das Projekt '{df['Prioritaet_Leerstand'].mode()[0]}' ist ein Gewinnerthema. Nutze es als dein Leuchtturmprojekt.")

    # Empfehlungen
    st.subheader("🚀 Strategische Empfehlungen")
    st.write("""
    1. **Fokus Naturschutz:** Dies ist ein Top-Thema über alle Gruppen hinweg.
    2. **Senioren-Strategie:** Die größte Wählergruppe (61+) sorgt sich um die Nahversorgung.
    3. **Finanzierung:** Die geringe Ablehnung beim Wasserverkauf bietet Spielraum für Budgetverhandlungen.
    """)
