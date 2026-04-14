# Project
Coding 
import folium
import os
import webbrowser
from folium import Element

# =========================
# BASE MAP (FIXED + LOOPING)
# =========================
m = folium.Map(
    location=[20, 0],
    zoom_start=2,
    tiles="CartoDB Positron",
    width="100%",
    height="100vh",
    world_copy_jump=True,
    no_wrap=False
)

# =========================
# FULL DATA (ALL AIRPORTS)
# =========================
smart_airports = [
    {
        "Rank": 1,
        "Name": "Incheon Airport",
        "Location": "South Korea",
        "Smart Technologies": "IoT integration, automated immigration, digital wayfinding",
        "Additional Details": "Facial recognition SmartPass, AI robots, autonomous shuttle buses",
        "lat": 37.4691, "lon": 126.4505
    },
    {
        "Rank": 2,
        "Name": "Hong Kong International Airport",
        "Location": "Hong Kong",
        "Smart Technologies": "Biometric check‑in, Flight Token Travel",
        "Additional Details": "CT‑based smart security screening",
        "lat": 22.3080, "lon": 113.9146
    },
    {
        "Rank": 3,
        "Name": "Amsterdam Schiphol Airport",
        "Location": "Netherlands",
        "Smart Technologies": "Smart grid, intelligent lighting",
        "Additional Details": "IoT networks and collaborative robots",
        "lat": 52.3086, "lon": 4.7639
    },
    {
        "Rank": 4,
        "Name": "Hamad International Airport",
        "Location": "Qatar",
        "Smart Technologies": "Biometrics, automation, AI services",
        "Additional Details": "Real‑time baggage tracking",
        "lat": 25.2731, "lon": 51.6081
    },
    {
        "Rank": 5,
        "Name": "Tokyo Haneda Airport",
        "Location": "Japan",
        "Smart Technologies": "Automated check‑in, biometrics",
        "Additional Details": "Facial recognition security systems",
        "lat": 35.5494, "lon": 139.7798
    },
    {
        "Rank": 6,
        "Name": "Munich Airport",
        "Location": "Germany",
        "Smart Technologies": "Smart parking, AI maintenance",
        "Additional Details": "Predictive infrastructure analytics",
        "lat": 48.3538, "lon": 11.7861
    },
    {
        "Rank": 7,
        "Name": "San Francisco International Airport",
        "Location": "USA",
        "Smart Technologies": "AI chatbots, smart baggage handling",
        "Additional Details": "Reduced lost luggage incidents",
        "lat": 37.6152, "lon": -122.3910
    }
]

sustainable_airports = [
    {
        "Rank": 1,
        "Name": "Denver International Airport",
        "Location": "USA",
        "Sustainable Elements": "Largest airport solar power farm",
        "Additional Details": "150‑acre solar array and recycling",
        "lat": 39.8561, "lon": -104.6737
    },
    {
        "Rank": 2,
        "Name": "Stockholm Arlanda Airport",
        "Location": "Sweden",
        "Sustainable Elements": "Energy‑efficient lighting",
        "Additional Details": "Smart lighting and recycling programs",
        "lat": 59.6519, "lon": 17.9186
    },
    {
        "Rank": 3,
        "Name": "Indira Gandhi International Airport",
        "Location": "India",
        "Sustainable Elements": "Solar power, green buildings",
        "Additional Details": "LEED‑certified terminals",
        "lat": 28.5665, "lon": 77.1031
    },
    {
        "Rank": 4,
        "Name": "Galapagos Ecological Airport",
        "Location": "Galapagos Islands",
        "Sustainable Elements": "100% renewable energy",
        "Additional Details": "Carbon‑neutral operations",
        "lat": -0.4538, "lon": -90.2659
    },
    {
        "Rank": 5,
        "Name": "Oslo Airport",
        "Location": "Norway",
        "Sustainable Elements": "Hydropower and AI HVAC systems",
        "Additional Details": "Energy‑efficient operations",
        "lat": 60.1939, "lon": 11.1004
    },
    {
        "Rank": 6,
        "Name": "Boston Logan International Airport",
        "Location": "USA",
        "Sustainable Elements": "Water conservation programs",
        "Additional Details": "Rainwater harvesting systems",
        "lat": 42.3643, "lon": -71.0052
    },
    {
        "Rank": 7,
        "Name": "San Diego International Airport",
        "Location": "USA",
        "Sustainable Elements": "Zero‑waste initiatives",
        "Additional Details": "Energy‑efficient terminal systems",
        "lat": 32.7336, "lon": -117.1897
    }
]

hybrid_airports = [
    {
        "Rank": 1,
        "Name": "Singapore Changi Airport",
        "Location": "Singapore",
        "Smart Technologies": "Biometrics, AI automation",
        "Sustainable Elements": "Solar panels, rainwater harvesting",
        "Additional Details": "Jewel Changi green architecture",
        "lat": 1.3644, "lon": 103.9915
    },
    {
        "Rank": 2,
        "Name": "Dubai International Airport",
        "Location": "UAE",
        "Smart Technologies": "Smart Corridor, AI services",
        "Sustainable Elements": "Electric vehicles and recycling",
        "Additional Details": "Zero‑waste strategy",
        "lat": 25.2528, "lon": 55.3644
    },
    {
        "Rank": 3,
        "Name": "Zurich Airport",
        "Location": "Switzerland",
        "Smart Technologies": "Digital services, automation",
        "Sustainable Elements": "Geothermal energy",
        "Additional Details": "Highly efficient operations",
        "lat": 47.4647, "lon": 8.5492
    }
]

# =========================
# YOUR POPUP LOGIC (UNCHANGED)
# =========================
def create_popup_content(airport, category):
    html = f"""
        <b>{airport['Name']}</b> ({category})<br>
        <b>Rank:</b> {airport['Rank']}<br>
        <b>Location:</b> {airport['Location']}<br>
    """
    if category in ["Smart", "Hybrid"]:
        html += f"<b>Smart Technologies:</b> {airport['Smart Technologies']}<br>"
    if category in ["Sustainable", "Hybrid"]:
        html += f"<b>Sustainable Elements:</b> {airport['Sustainable Elements']}<br>"
    html += f"<b>Additional Details:</b> {airport['Additional Details']}"
    return html

# =========================
# ADD MARKERS
# =========================
for a in smart_airports:
    folium.Marker([a["lat"], a["lon"]],
        popup=folium.Popup(create_popup_content(a, "Smart"), max_width=350),
        icon=folium.Icon(color="blue", icon="plane", prefix="fa")
    ).add_to(m)

for a in sustainable_airports:
    folium.Marker([a["lat"], a["lon"]],
        popup=folium.Popup(create_popup_content(a, "Sustainable"), max_width=350),
        icon=folium.Icon(color="green", icon="leaf", prefix="fa")
    ).add_to(m)

for a in hybrid_airports:
    folium.Marker([a["lat"], a["lon"]],
        popup=folium.Popup(create_popup_content(a, "Hybrid"), max_width=350),
        icon=folium.Icon(color="purple", icon="plane", prefix="fa")
    ).add_to(m)

# =========================
# SAVE & OPEN
# =========================
output = os.path.join(os.path.expanduser("~"), "Desktop", "BevanHP_ALL_Airports_FINAL.html")
m.save(output)
webbrowser.open(output)

print("✅ All airports loaded successfully:", output)






#############check box 


import folium
import os
import webbrowser
from folium import Element

# =========================
# BASE MAP (GOOGLE-MAP STYLE)
# =========================
m = folium.Map(
    location=[20, 0],
    zoom_start=2,
    tiles="CartoDB Positron",
    width="100%",
    height="100vh",
    world_copy_jump=True,
    no_wrap=False
)

# =========================
# DATA WITH ONLINE IMAGES
# =========================
smart_airports = [
    {
        "Rank": 1,
        "Name": "Incheon Airport",
        "Location": "South Korea",
        "Smart Technologies": "IoT integration, automated immigration, digital wayfinding",
        "Additional Details": "Facial recognition SmartPass and AI robots",
        "Image": "https://upload.wikimedia.org/wikipedia/commons/5/5a/Incheon_International_Airport_T2.jpg",
        "lat": 37.4691,
        "lon": 126.4505
    },
    {
        "Rank": 2,
        "Name": "Hong Kong International Airport",
        "Location": "Hong Kong",
        "Smart Technologies": "Biometric check-in and Flight Token Travel",
        "Additional Details": "CT-based smart security screening",
        "Image": "https://tse4.mm.bing.net/th/id/OIP.K-e8XhgSWed7ZOATlOcQtwHaE7?rs=1&pid=ImgDetMain&o=7&rm=3",
        "lat": 22.3080,
        "lon": 113.9146
    }
]

sustainable_airports = [
    {
        "Rank": 1,
        "Name": "Denver International Airport",
        "Location": "USA",
        "Sustainable Elements": "Largest airport solar power farm",
        "Additional Details": "150-acre solar array and recycling systems",
        "Image": "https://upload.wikimedia.org/wikipedia/commons/8/85/Denver_International_Airport_terminal.jpg",
        "lat": 39.8561,
        "lon": -104.6737
    }
]

hybrid_airports = [
    {
        "Rank": 1,
        "Name": "Singapore Changi Airport",
        "Location": "Singapore",
        "Smart Technologies": "Biometrics and AI automation",
        "Sustainable Elements": "Solar panels and rainwater harvesting",
        "Additional Details": "Jewel Changi sustainable architecture",
        "Image": "https://upload.wikimedia.org/wikipedia/commons/1/1f/Jewel_Changi_Airport.jpg",
        "lat": 1.3644,
        "lon": 103.9915
    }
]

# ==================================================
# ✅ YOUR POPUP LOGIC (WITH IMAGE SUPPORT)
# ==================================================
def create_popup_content(airport, category):
    html = f"""
        <b>{airport['Name']}</b> ({category})<br>
        <b>Rank:</b> {airport['Rank']}<br>
        <b>Location:</b> {airport['Location']}<br><br>
    """

    # ✅ IMAGE
    if "Image" in airport:
        html += f"""
        <img src="{airport['Image']}"
             style="width:100%; max-width:300px; border-radius:8px;"><br><br>
        """

    if category in ["Smart", "Hybrid"]:
        html += f"<b>Smart Technologies:</b> {airport['Smart Technologies']}<br>"

    if category in ["Sustainable", "Hybrid"]:
        html += f"<b>Sustainable Elements:</b> {airport['Sustainable Elements']}<br>"

    html += f"<b>Additional Details:</b> {airport['Additional Details']}"
    return html

# =========================
# LAYERS (FOR CHECKBOX CONTROL)
# =========================
smart_layer = folium.FeatureGroup(name="Smart Airports")
sustainable_layer = folium.FeatureGroup(name="Sustainable Airports")
hybrid_layer = folium.FeatureGroup(name="Hybrid Airports")

for a in smart_airports:
    folium.Marker(
        [a["lat"], a["lon"]],
        popup=folium.Popup(create_popup_content(a, "Smart"), max_width=350),
        icon=folium.Icon(color="blue", icon="plane", prefix="fa")
    ).add_to(smart_layer)

for a in sustainable_airports:
    folium.Marker(
        [a["lat"], a["lon"]],
        popup=folium.Popup(create_popup_content(a, "Sustainable"), max_width=350),
        icon=folium.Icon(color="green", icon="leaf", prefix="fa")
    ).add_to(sustainable_layer)

for a in hybrid_airports:
    folium.Marker(
        [a["lat"], a["lon"]],
        popup=folium.Popup(create_popup_content(a, "Hybrid"), max_width=350),
        icon=folium.Icon(color="purple", icon="plane", prefix="fa")
    ).add_to(hybrid_layer)

smart_layer.add_to(m)
sustainable_layer.add_to(m)
hybrid_layer.add_to(m)

# =========================
# LAYER CONTROL (LIKE GOOGLE MAP)
# =========================
folium.LayerControl(collapsed=False).add_to(m)

# =========================
# RESIZE FIX
# =========================
resize_fix = Element("""
<script>
setTimeout(function() {
    window.dispatchEvent(new Event('resize'));
}, 500);
</script>
""")
m.get_root().html.add_child(resize_fix)

# =========================
# SAVE & OPEN
# =========================
output_path = os.path.join(
    os.path.expanduser("~"),
    "Desktop",
    "BevanHP_Airports_With_Photos.html"
)

m.save(output_path)
webbrowser.open(output_path)

print("✅ Map created with image popups:", output_path)
