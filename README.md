import streamlit as st
from openai import OpenAI

client = OpenAI(api_key=st.secrets["OPENAI_API_KEY"])

st.set_page_config(page_title="Meesho AI SEO", page_icon="🔥")

st.title("🔥 Meesho AI SEO Generator")

product = st.text_input("Product Name")
category = st.text_input("Category")
fabric = st.text_input("Fabric")
color = st.text_input("Color")
price = st.text_input("Price Range")

if st.button("Generate SEO"):
    if product == "":
        st.warning("Product name দে আগে")
    else:
        prompt = f"""
        You are a Meesho SEO expert.
        Generate:
        1. 5 trending Meesho keywords
        2. 1 SEO title (under 150 characters)
        3. Product description in English with bullet points

        Product: {product}
        Category: {category}
        Fabric: {fabric}
        Color: {color}
        Price: {price}
        """

        response = client.chat.completions.create(
            model="gpt-4o-mini",
            messages=[{"role": "user", "content": prompt}]
        )

        st.success("✅ Generated Successfully")
        st.write(response.choices[0].message.content)
