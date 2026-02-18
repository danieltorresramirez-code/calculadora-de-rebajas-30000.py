import streamlit as st


## 1. Configuración de la página
st.set_page_config(page_title="Calculadora de Rebajas", page_icon="🏷️")

# Título y Descripción
st.title("🛍️ Calculadora de Ofertas")
st.markdown("Calcula cuánto te ahorras y cuál es el precio final de tus caprichos.")
st.write("---") 

# 2. Entrada de Datos (Barra Lateral)
st.sidebar.header("Detalles del Producto")
precio_original = st.sidebar.number_input("Precio original (€)", min_value=0.0, value=50.0, step=0.5)
descuento = st.sidebar.slider("Porcentaje de descuento (%)", 0, 90, 20)

# 3. Lógica y Botón de Cálculo
if st.button("Aplicar Descuento"):
    
    # Cálculo matemático
    ahorro = precio_original * (descuento / 100)
    precio_final = precio_original - ahorro
    
    # 4. Mostrar Resultado con Diseño
    col1, col2 = st.columns(2)
    
    with col1:
        # Mostramos el precio final en grande
        st.metric(label="Precio Final", value=f"{precio_final:.2f} €", delta=f"-{ahorro:.2f} €")
        
    with col2:
        # Diagnóstico de la oferta según el porcentaje
        if descuento >= 70:
            st.error("🔥 ¡CHOLLO EXTREMO!")
            st.balloons() 
        elif 40 <= descuento < 70:
            st.success("✅ ¡Gran Oportunidad!")
        elif 10 <= descuento < 40:
            st.warning("🟠 Descuento Estándar")
        else:
            st.info("ℹ️ Rebaja mínima")

    # Extra: Resumen visual
    st.write("---")
    st.info(f"Estás pagando solo el **{100 - descuento}%** del valor original.")
    
    # Fórmula matemática en LaTeX
    st.latex(r''' Precio_{final} = Precio_{orig} - \left( Precio_{orig} \cdot \frac{\%Desc}{100} \right) ''')
