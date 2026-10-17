# Free-tool-finder-AI
My first project AI tool recommemder
I’m ready to set this up, but I can’t complete the repository creation from this chat right now because the required action is currently blocked in this session. Please do this instead in your own environment:

1) Create a new public GitHub repo named:
   free-tool-finder-app

2) Create a file named:
   app.py

3) Paste this exact content into app.py:

```python
import streamlit as st
import pandas as pd
import json

# Page Configuration
st.set_page_config(
    page_title="Free Tool Finder AI",
    page_icon="🤖",
    layout="wide",
    initial_sidebar_state="expanded"
)

# Header
st.title("🤖 Free Tool Finder AI")
st.caption("Centralized AI Tool Discovery, Scoring Recommendation Engine, Workflow Planner & Prompt Architect")
st.caption("College Project by: Jayasimman.L | Hema Priyan.K | Lokesh.E | Jacob Livingstone.R (Sri Ramanujar Engineering College)")

# Tool Catalog Dataset
@st.cache_data
def get_tools_database():
    return [
        {
            "id": 1,
            "name": "CapCut",
            "icon": "🎬",
            "category": "Video",
            "description": "All-in-one AI video editor with auto-captions, background removal, voice synth, and video generation.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Supported",
            "features": ["Auto Captions", "Background Removal", "AI Video Effects", "Mobile & Web", "4K Export"],
            "official_url": "CapCut Official Platform",
            "review_url": "CapCut Video Tutorial"
        },
        {
            "id": 2,
            "name": "Clipchamp",
            "icon": "📹",
            "category": "Video",
            "description": "Microsoft free online video editor featuring AI text-to-speech, auto-cropping, and template creation.",
            "free_status": "Free",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Web Only",
            "features": ["1080p Free Export", "Text-to-Speech", "Stock Footage", "No Watermark", "Screen Recorder"],
            "official_url": "Clipchamp Studio",
            "review_url": "Clipchamp Video Tutorial"
        },
        {
            "id": 3,
            "name": "Runway ML (Gen-2)",
            "icon": "🎥",
            "category": "Video",
            "description": "Multimodal AI video generation platform generating videos from text, images, or video clips.",
            "free_status": "Free Tier",
            "watermark_status": "Watermark on Free",
            "commercial_status": "Personal Only",
            "mobile_status": "Supported",
            "features": ["Text to Video", "Image to Video", "Motion Brush", "Gen-2 Engine", "Inpainting"],
            "official_url": "Runway ML Platform",
            "review_url": "Runway ML Video Tutorial"
        },
        {
            "id": 4,
            "name": "Canva Magic Studio",
            "icon": "🎨",
            "category": "Design/3D",
            "description": "Comprehensive design suite with AI image generation, background eraser, magic edit, and brand kits.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Supported",
            "features": ["Magic Media", "Background Remover", "Templates", "Social Media Graphics", "Brand Kit"],
            "official_url": "Canva Magic Studio",
            "review_url": "Canva Studio Video Tutorial"
        },
        {
            "id": 5,
            "name": "Adobe Express",
            "icon": "📐",
            "category": "Design/3D",
            "description": "Free web and mobile design app powered by Adobe Firefly AI for text-to-image and text effects.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Supported",
            "features": ["Adobe Firefly Powered", "Text to Image", "Generative Fill", "Commercial Safe", "Social Templates"],
            "official_url": "Adobe Express App",
            "review_url": "Adobe Express Video Tutorial"
        },
        {
            "id": 6,
            "name": "Leonardo.ai",
            "icon": "🖼️",
            "category": "Image",
            "description": "Generative AI art platform with daily free tokens, custom model fine-tuning, and ultra-high resolution generation.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Supported",
            "features": ["150 Daily Tokens", "Custom Models", "Alchemy Upscale", "Canvas Editor", "PNG Export"],
            "official_url": "Leonardo AI Studio",
            "review_url": "Leonardo AI Video Tutorial"
        },
        {
            "id": 7,
            "name": "Hugging Face Chat & Spaces",
            "icon": "🤗",
            "category": "Image",
            "description": "Open-source community platform offering free access to Stable Diffusion models, FLUX, and LLMs.",
            "free_status": "Free",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Web Only",
            "features": ["FLUX.1 Access", "Stable Diffusion XL", "Open Source Models", "No Restrictions", "Community Demos"],
            "official_url": "Hugging Face Community",
            "review_url": "Hugging Face Video Tutorial"
        },
        {
            "id": 8,
            "name": "ElevenLabs",
            "icon": "🎙️",
            "category": "Audio",
            "description": "Industry-leading AI voice generator and text-to-speech platform with realistic voice synthesis.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Personal Only",
            "mobile_status": "Supported",
            "features": ["Realistic Voice Cloning", "Multilingual Speech", "10k Free Characters/Mo", "Voice Library", "Audio Native"],
            "official_url": "ElevenLabs Voice Platform",
            "review_url": "ElevenLabs Video Tutorial"
        },
        {
            "id": 9,
            "name": "Audacity with OpenVINO AI",
            "icon": "🎧",
            "category": "Audio",
            "description": "Free open-source audio editor equipped with AI plugins for noise suppression, stem separation, and transcription.",
            "free_status": "Free",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Web Only",
            "features": ["100% Free Open Source", "Stem Separation", "Noise Removal", "Local Execution", "Unlimited Export"],
            "official_url": "Audacity Open Source Project",
            "review_url": "Audacity AI Video Tutorial"
        },
        {
            "id": 10,
            "name": "ChatGPT (GPT-4o mini)",
            "icon": "💬",
            "category": "Writing/Research",
            "description": "Versatile AI assistant for content writing, brainstorming, research, code generation, and complex analysis.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Supported",
            "features": ["GPT-4o mini Access", "Web Search", "Data Analysis", "Code Interpreter", "iOS/Android Apps"],
            "official_url": "ChatGPT Portal",
            "review_url": "ChatGPT Video Tutorial"
        },
        {
            "id": 11,
            "name": "Claude 3.5 Sonnet",
            "icon": "✍️",
            "category": "Writing/Research",
            "description": "Advanced AI model known for superior creative writing, nuanced research, coding accuracy, and long context understanding.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Supported",
            "features": ["Artifacts Interactive View", "Long Context Window", "Nuanced Writing", "Code Generation", "Free Daily Messages"],
            "official_url": "Claude AI Portal",
            "review_url": "Claude AI Video Tutorial"
        },
        {
            "id": 12,
            "name": "GitHub Copilot Free Tier",
            "icon": "💻",
            "category": "Coding",
            "description": "AI developer pair programmer providing code auto-completions, inline chat, and test generation in VS Code.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Web Only",
            "features": ["Inline Code Completion", "VS Code Extension", "Multi-language Support", "Chat Assistant", "Refactoring"],
            "official_url": "GitHub Copilot Platform",
            "review_url": "GitHub Copilot Video Tutorial"
        },
        {
            "id": 13,
            "name": "Cursor IDE",
            "icon": "⚡",
            "category": "Coding",
            "description": "AI-first code editor built on VS Code with codebase index search, multi-file edits, and instant terminal fix.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Allowed",
            "mobile_status": "Web Only",
            "features": ["Full Codebase Context", "Cmd+K Inline Edit", "Multi-file Refactoring", "VS Code Compatible", "Terminal Assistant"],
            "official_url": "Cursor IDE Portal",
            "review_url": "Cursor IDE Video Tutorial"
        },
        {
            "id": 14,
            "name": "Suno AI",
            "icon": "🎵",
            "category": "Audio",
            "description": "Generate full songs with vocals, lyrics, and instrumentals in any genre from simple text prompts.",
            "free_status": "Free Tier",
            "watermark_status": "No Watermark",
            "commercial_status": "Personal Only",
            "mobile_status": "Supported",
            "features": ["50 Daily Free Credits", "Full Song Generation", "Custom Lyrics", "Genre Selection", "MP3 Download"],
            "official_url": "Suno Music AI",
            "review_url": "Suno AI Video Tutorial"
        }
    ]

# Matching Score Engine
def calculate_matching_score(tool, query):
    if not query or query.strip() == "":
        return 50
    
    q_lower = query.lower()
    score = 40  # Base Score = 40

    cat_lower = tool['category'].lower()
    
    # Category match (+30)
    category_keywords = {
        "video": ["video", "animation", "movie", "film", "clip", "editor", "vlog"],
        "image": ["image", "photo", "picture", "art", "drawing", "illustration", "graphic"],
        "audio": ["audio", "voice", "speech", "sound", "music", "podcast", "tts"],
        "coding": ["code", "coding", "developer", "program", "python", "software", "ide", "vscode"],
        "writing/research": ["write", "writing", "essay", "text", "research", "blog", "summary", "article"],
        "design/3d": ["design", "3d", "ui", "ux", "template", "poster", "banner", "logo"]
    }
    
    if cat_lower in q_lower or any(syn in q_lower for syn in category_keywords.get(cat_lower, [])):
        score += 30

    # Keyword match (+8)
    tool_text = (tool['name'] + " " + tool['description'] + " " + " ".join(tool['features'])).lower()
    query_words = [w for w in q_lower.split() if len(w) > 2]
    matching_words = [w for w in query_words if w in tool_text]
    if matching_words:
        score += 8

    # Free requirement (+10)
    if any(k in q_lower for k in ["free", "no cost", "0\$", "freemium"]):
        if tool['free_status'] in ["Free", "Free Tier", "Freemium"]:
            score += 10

    # Watermark requirement (+10)
    if any(k in q_lower for k in ["no watermark", "watermark free", "without watermark", "clean"]):
        if tool['watermark_status'] == "No Watermark":
            score += 10

    # Commercial requirement (+10)
    if any(k in q_lower for k in ["commercial", "monetize", "business", "commercial use", "sell"]):
        if tool['commercial_status'] == "Allowed":
            score += 10

    # Mobile requirement (+8)
    if any(k in q_lower for k in ["mobile", "app", "phone", "android", "ios"]):
        if tool['mobile_status'] == "Supported":
            score += 8

    # Cap score at 100
    return min(100, score)

# Session State Initializers
if 'saved_tool_ids' not in st.session_state:
    st.session_state.saved_tool_ids = [1, 4, 10]

if 'selected_compare_ids' not in st.session_state:
    st.session_state.selected_compare_ids = [1, 2]

if 'quick_cat' not in st.session_state:
    st.session_state.quick_cat = "All"

# Tabs Setup
tab_search, tab_filter, tab_compare, tab_saved, tab_workflow, tab_architect = st.tabs([
    "🔍 Search & Recommend",
    "🎛️ Advanced Filters",
    "⚖️ Tool Comparison",
    "⭐ Saved Tools",
    "🔄 Workflow Planner",
    "🏗️ Software Prompt Architect"
])

# -------------------------------------------------------------
# TAB 1: SEARCH & RECOMMENDATION ENGINE
# -------------------------------------------------------------
with tab_search:
    st.subheader("Natural Language AI Tool Discovery")
    
    col_input, col_btn = st.columns([5, 1])
    with col_input:
        search_query = st.text_input(
            "Enter your project requirement:",
            value="Free AI video generator without watermark for commercial use",
            key="main_search_input"
        )
    with col_btn:
        st.write("<div style='height: 28px;'></div>", unsafe_allow_html=True)
        search_trigger = st.button("🔍 Find Tools", use_container_width=True, type="primary")

    st.write("**Quick Category Selection:**")
    categories = ["All", "Video", "Image", "Audio", "Coding", "Writing/Research", "Design/3D"]
    cat_cols = st.columns(len(categories))
    
    for idx, cat in enumerate(categories):
        btn_type = "primary" if st.session_state.quick_cat == cat else "secondary"
        if cat_cols[idx].button(cat, key=f"cat_btn_{cat}", use_container_width=True, type=btn_type):
            st.session_state.quick_cat = cat
            st.rerun()

    tools = get_tools_database()
    
    scored_tools = []
    for t in tools:
        if st.session_state.quick_cat != "All" and t['category'] != st.session_state.quick_cat:
            continue
        
        score = calculate_matching_score(t, search_query)
        scored_tools.append((score, t))
    
    scored_tools.sort(key=lambda x: x[0], reverse=True)
    
    st.markdown(f"### Recommended Tools ({len(scored_tools)} tools matched)")

    for score, tool in scored_tools:
        is_saved = tool['id'] in st.session_state.saved_tool_ids
        
        with st.container(border=True):
            col_icon, col_details, col_actions = st.columns([1, 6, 2])
            
            with col_icon:
                st.title(f"{tool['icon']}")
            
            with col_details:
                st.markdown(f"### {tool['name']}  `{tool['category']}`  *(Match Score: {score}%)*")
                st.write(tool['description'])
                
                c1, c2, c3, c4 = st.columns(4)
                c1.info(f"Tier: {tool['free_status']}")
                c2.success(f"Watermark: {tool['watermark_status']}")
                c3.warning(f"Commercial: {tool['commercial_status']}")
                c4.error(f"Mobile: {tool['mobile_status']}")
                
                st.write("Features: " + ", ".join([f"`#{f}`" for f in tool['features']]))
                
            with col_actions:
                st.write(f"🌐 Official: {tool['official_url']}")
                st.write(f"▶️ Tutorial: {tool['review_url']}")
                
                if is_saved:
                    if st.button("⭐ Saved", key=f"unsave_{tool['id']}", use_container_width=True, type="secondary"):
                        st.session_state.saved_tool_ids.remove(tool['id'])
                        st.rerun()
                else:
                    if st.button("☆ Save Tool", key=f"save_{tool['id']}", use_container_width=True):
                        st.session_state.saved_tool_ids.append(tool['id'])
                        st.rerun()

# -------------------------------------------------------------
# TAB 2: ADVANCED FILTERS
# -------------------------------------------------------------
with tab_filter:
    st.subheader("🎛️ Requirement Filter Matrix")
    
    col_f1, col_f2, col_f3, col_f4 = st.columns(4)
    with col_f1:
        f_category = st.selectbox("Category Filter", ["All", "Video", "Image", "Audio", "Coding", "Writing/Research", "Design/3D"])
    with col_f2:
        f_free = st.selectbox("Pricing Tier", ["All", "Free", "Free Tier", "Freemium"])
    with col_f3:
        f_watermark = st.selectbox("Watermark Filter", ["All", "No Watermark Only"])
    with col_f4:
        f_commercial = st.selectbox("Commercial License", ["All", "Allowed Only"])
        
    f_mobile = st.checkbox("📱 Must support Mobile Devices")
    
    filtered_list = []
    for tool in get_tools_database():
        if f_category != "All" and tool['category'] != f_category:
            continue
        if f_free != "All" and tool['free_status'] != f_free:
            continue
        if f_watermark == "No Watermark Only" and tool['watermark_status'] != "No Watermark":
            continue
        if f_commercial == "Allowed Only" and tool['commercial_status'] != "Allowed":
            continue
        if f_mobile and tool['mobile_status'] != "Supported":
            continue
        filtered_list.append(tool)
        
    st.write(f"### Filtered Results ({len(filtered_list)} matches)")
    
    if filtered_list:
        df_filtered = pd.DataFrame([{
            "Icon": t['icon'],
            "Name": t['name'],
            "Category": t['category'],
            "Free Tier": t['free_status'],
            "Watermark": t['watermark_status'],
            "Commercial Use": t['commercial_status'],
            "Mobile Support": t['mobile_status'],
            "Official Link": t['official_url']
        } for t in filtered_list])
        
        st.dataframe(df_filtered, use_container_width=True, hide_index=True)
    else:
        st.warning("No tools match all selected strict filters. Try loosening criteria.")

# -------------------------------------------------------------
# TAB 3: SIDE-BY-SIDE TOOL COMPARISON
# -------------------------------------------------------------
with tab_compare:
    st.subheader("⚖️ Side-by-Side Tool Comparison Engine")
    
    tools_all = get_tools_database()
    tool_options = {f"{t['icon']} {t['name']} ({t['category']})": t['id'] for t in tools_all}
    
    default_selected = [k for k, v in tool_options.items() if v in st.session_state.selected_compare_ids]
    
    selected_labels = st.multiselect(
        "Select 2 to 4 AI Tools to Compare:",
        options=list(tool_options.keys()),
        default=default_selected
    )
    
    selected_ids = [tool_options[label] for label in selected_labels]
    st.session_state.selected_compare_ids = selected_ids
    
    if len(selected_ids) >= 2:
        comp_tools = [t for t in tools_all if t['id'] in selected_ids]
        
        comp_data = {
            "Attribute": [
                "Category",
                "Description",
                "Free Plan Status",
                "Watermark Policy",
                "Commercial Rights",
                "Mobile Support",
                "Key Features",
                "Official Website"
            ]
        }
        
        for t in comp_tools:
            comp_data[f"{t['icon']} {t['name']}"] = [
                t['category'],
                t['description'],
                t['free_status'],
                t['watermark_status'],
                t['commercial_status'],
                t['mobile_status'],
                ", ".join(t['features']),
                t['official_url']
            ]
            
        df_comp = pd.DataFrame(comp_data)
        st.table(df_comp)
    else:
        st.info("Please select at least 2 tools to generate a side-by-side comparison table.")

# -------------------------------------------------------------
# TAB 4: SAVED TOOLS MANAGEMENT
# -------------------------------------------------------------
with tab_saved:
    st.subheader("⭐ Bookmarked AI Tools Collection")
    
    tools_all = get_tools_database()
    saved_tools = [t for t in tools_all if t['id'] in st.session_state.saved_tool_ids]
    
    if saved_tools:
        st.write(f"You have **{len(saved_tools)}** saved tools in your collection.")
        
        col_s_left, col_s_right = st.columns([3, 1])
        with col_s_right:
            json_str = json.dumps(saved_tools, indent=2)
            st.download_button(
                "📥 Export Saved Tools (JSON)",
                data=json_str,
                file_name="free_tool_finder_saved_tools.json",
                mime="application/json",
                use_container_width=True
            )
            
        for tool in saved_tools:
            with st.expander(f"{tool['icon']} {tool['name']} — {tool['category']}", expanded=True):
                st.write(tool['description'])
                st.markdown(f"**Pricing:** {tool['free_status']} | **Watermark:** {tool['watermark_status']} | **Commercial:** {tool['commercial_status']} | **Mobile:** {tool['mobile_status']}")
                
                c1, c2, c3 = st.columns(3)
                c1.write(f"🌐 Site: {tool['official_url']}")
                c2.write(f"▶️ Review: {tool['review_url']}")
                if c3.button("🗑️ Remove", key=f"rem_saved_{tool['id']}", use_container_width=True):
                    st.session_state.saved_tool_ids.remove(tool['id'])
                    st.rerun()
    else:
        st.info("No tools saved yet. Click '☆ Save Tool' on any search result to add it to your saved collection.")

# -------------------------------------------------------------
# TAB 5: MULTI-TOOL WORKFLOW PLANNER
# -------------------------------------------------------------
with tab_workflow:
    st.subheader("🔄 Multi-Tool Workflow Execution Planner")
    st.write("Combine multiple specialized AI tools into a seamless, step-by-step project execution pipeline.")
    
    preset_goals = [
        "🎬 Complete YouTube Video Creation Pipeline",
        "💻 Full-Stack SaaS Application Development",
        "📚 E-Book & Technical Content Publishing",
        "🎙️ Podcast Production & Audio Distribution",
        "Custom Project Workflow"
    ]
    
    selected_goal = st.selectbox("Select Project Objective:", preset_goals)
    
    if "YouTube Video" in selected_goal:
        steps = [
            {"phase": "Phase 1: Idea & Scriptwriting", "tool": "ChatGPT (GPT-4o mini) / Claude 3.5", "icon": "✍️", "action": "Generate video outline, hook, full script, and scene visual descriptions.", "output": "Script & Scene Document"},
            {"phase": "Phase 2: Voiceover & Audio", "tool": "ElevenLabs / Suno AI", "icon": "🎙️", "action": "Convert script text to realistic AI voiceover and background music track.", "output": "Voiceover MP3 & Music Files"},
            {"phase": "Phase 3: Visual & Video Assets", "tool": "Runway ML (Gen-2) / Leonardo.ai", "icon": "🎥", "action": "Generate AI video clips and thumbnail artwork using prompts.", "output": "MP4 Clips & Thumbnail PNG"},
            {"phase": "Phase 4: Editing & Auto-Captions", "tool": "CapCut / Clipchamp", "icon": "🎬", "action": "Assemble voiceover, video clips, B-roll, music, auto-captions, and export.", "output": "Final Master YouTube MP4 Video"}
        ]
    elif "SaaS Application" in selected_goal:
        steps = [
            {"phase": "Phase 1: System Architecture", "tool": "Claude 3.5 Sonnet / Software Prompt Architect", "icon": "🏗️", "action": "Define database schema, API route structure, and system prompts.", "output": "Architecture Blueprint"},
            {"phase": "Phase 2: Core Frontend & UI Design", "tool": "Canva Magic Studio / Adobe Express", "icon": "📐", "action": "Mockup UI/UX screens, brand assets, icons, and color palette.", "output": "UI Wireframes & Assets"},
            {"phase": "Phase 3: Codebase Implementation", "tool": "Cursor IDE / GitHub Copilot", "icon": "💻", "action": "Autogenerate REST endpoints, React components, and ORM models.", "output": "Full Repository Source Code"},
            {"phase": "Phase 4: Demo Video & Launch", "tool": "Clipchamp / Adobe Express", "icon": "📹", "action": "Record screen demo, generate launch video, and export marketing assets.", "output": "Product Demo Video"}
        ]
    else:
        steps = [
            {"phase": "Step 1: Planning & Research", "tool": "ChatGPT / Claude 3.5", "icon": "💡", "action": "Gather reference data, structure outline, and draft blueprint.", "output": "Project Plan Document"},
            {"phase": "Step 2: Asset Creation", "tool": "Leonardo.ai / ElevenLabs", "icon": "🎨", "action": "Generate images, sound effects, or visual elements.", "output": "Asset Library"},
            {"phase": "Step 3: Assembly & Output", "tool": "CapCut / Canva", "icon": "🛠️", "action": "Combine text, assets, and design elements into final deliverable.", "output": "Final Deliverable"}
        ]
        
    st.write("#### Generated Step-by-Step Multi-Tool Pipeline:")
    for idx, s in enumerate(steps, 1):
        with st.container(border=True):
            st.markdown(f"**Step {idx}: {s['phase']}**")
            st.write(f"Recommended Tool: {s['icon']} {s['tool']}")
            st.write(f"Action: {s['action']}")
            st.write(f"Expected Output: `{s['output']}`")

# -------------------------------------------------------------
# TAB 6: SOFTWARE PROMPT ARCHITECT
# -------------------------------------------------------------
with tab_architect:
    st.subheader("🏗️ Software Prompt Architect")
    st.write("Generate production-grade structured prompts for AI code assistants (Cursor, Copilot, ChatGPT, Claude).")
    
    col_p1, col_p2 = st.columns(2)
    with col_p1:
        p_title = st.text_input("Application Name:", value="Free Tool Finder AI")
        p_stack = st.selectbox("Tech Stack:", [
            "React + Node.js + Express + PostgreSQL",
            "Streamlit + Python + Pandas + SQLite",
            "Next.js (App Router) + Tailwind CSS + Supabase",
            "Vue.js + FastAPI + MongoDB"
        ])
        p_auth = st.selectbox("Authentication Strategy:", ["JWT Tokens", "OAuth 2.0 (Google/GitHub)", "Supabase Auth", "None (Public API)"])
        
    with col_p2:
        p_features = st.text_area("Core Features List (comma separated):", value="NL Requirement Search, 100-Point Match Score Engine, Side-by-Side Comparison Matrix, LocalStorage Saved Tools, Multi-Tool Workflow Generator")
        p_deploy = st.selectbox("Target Deployment Environment:", ["Vercel / Netlify", "Docker Container + AWS ECS", "Streamlit Cloud", "Render / Railway"])
        p_security = st.multiselect("Security & Quality Controls:", [
            "Input Sanitization & XSS Prevention",
            "Rate Limiting (100 req/min)",
            "Strict CORS Policies",
            "Environment Variable Secrets Isolation",
            "Jest / PyTest Unit Tests Coverage"
        ], default=["Input Sanitization & XSS Prevention", "Environment Variable Secrets Isolation"])

    if st.button("🚀 Generate Architect Mega-Prompt", type="primary", use_container_width=True):
        feature_lines = [f"- Feature {idx+1}: {feat.strip()}" for idx, feat in enumerate(p_features.split(','))]
        security_lines = [f"- {sec}" for sec in p_security]
        
        generated_prompt = f"""# SYSTEM DEVELOPMENT SPECIFICATION & INSTRUCTION PROMPT

## 1. PROJECT IDENTIFICATION & GOAL
- **Application Title**: {p_title}
- **Objective**: Build a high-performance web application providing requirement-based discovery, matching, comparison, and workflow planning.

## 2. TECH STACK ARCHITECTURE
- **Framework & Runtime**: {p_stack}
- **Authentication**: {p_auth}
- **Deployment Platform**: {p_deploy}

## 3. CORE FUNCTIONAL MODULES
""" + "\n".join(feature_lines) + f"""

## 4. MATCHING SCORING ALGORITHM REQUIREMENTS
Implement the scoring formula capped at 100 points:
- Base Score: 40 points
- Category Direct Match: +30 points
- Keyword Matching: +8 points
- Free Requirement: +10 points
- No Watermark Requirement: +10 points
- Commercial Requirement: +10 points
- Mobile Requirement: +8 points

## 5. SECURITY & COMPLIANCE MANDATES
""" + "\n".join(security_lines) + f"""

## 6. UI/UX & LAYOUT REQUIREMENTS
- Implement responsive theme palette (#0F172A background, #1E293B card containers, #38BDF8 accent highlight).
- Provide sticky filtering controls, multi-select comparison matrices, and clean overlays.

## 7. EXECUTION INSTRUCTIONS
Act as a Principal Full-Stack Software Architect. Write clean, modular, production-ready code with full error handling, type definitions, and detailed inline documentation.
"""
        st.success("Software Development Prompt Generated Successfully!")
        st.code(generated_prompt, language="markdown")
        
        st.download_button(
            "📋 Download Prompt File (.md)",
            data=generated_prompt,
            file_name=f"{p_title.lower().replace(' ', '_')}_architect_prompt.md",
            mime="text/markdown",
            use_container_width=True
        )
```




```bash
pip install streamlit pandas
streamlit run app.py
```

