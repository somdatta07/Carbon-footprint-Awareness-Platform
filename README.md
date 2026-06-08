🌱 Carbon Footprint Awareness Platform
Chosen Vertical
Climate Tech / Personal Sustainability
Carbon emissions from individual behaviour account for roughly 25–30% of global greenhouse gas output. Yet most people have little visibility into where their emissions come from, how they compare to others, or what actions would make the most meaningful difference. This platform bridges that gap with a smart, data-driven assistant.

Approach & Logic
The platform is built as a single-page React-style HTML/JS application with five integrated modules, powered by the Claude API for intelligent conversation. The design philosophy is context-aware guidance — each section feeds into the others, creating a coherent journey from awareness → calculation → action → habit formation.
Design Principles

Concrete over abstract — everything is quantified in tonnes CO₂e, not vague ratings
Actionable over educational — every insight connects to a specific next step
Encouraging over guilt-tripping — framing focuses on opportunity, not failure
Personalised over generic — the AI advisor receives user context (calculated footprint, lifestyle data) to give relevant advice


How the Solution Works
Module 1 — Dashboard
An at-a-glance overview of the user's carbon profile with:

4 key metrics: total footprint, comparison to global average, top two emission categories
Horizontal bar chart breaking down emissions by category (Chart.js)
6-month trend line showing reduction progress
Donut chart showing proportional category split
A contextual insight banner highlighting the single biggest reduction opportunity, with a direct link into the AI Advisor

Module 2 — Carbon Calculator
An interactive slider-based calculator covering all four major emission categories:
Transport

Car travel (km/week) × 0.17 kg CO₂e/km × 52 weeks
Flights per year × 0.30 tonnes CO₂e (average medium-haul)
Public transit (km/week) × 0.04 kg CO₂e/km × 52 weeks

Home Energy

Electricity (kWh/month) × 0.23 kg CO₂e/kWh × 12 months (India grid average)
Natural gas (m³/month) × 2.04 kg CO₂e/m³ × 12 months

Food & Diet

Diet-based emission factor: meat-heavy (3.3t) → vegan (1.1t) per year
Based on published lifecycle assessment data for dietary patterns

Shopping

Orders/month × 10 kg CO₂e/order × 12 months (average e-commerce parcel)

The calculator updates in real-time and classifies the result as Low / Moderate / High impact relative to global averages. A "Get personalised tips" button passes the full calculated profile into the AI Advisor as context.
Module 3 — AI Advisor (Claude-powered)
A conversational assistant powered by claude-sonnet-4-20250514 via the Anthropic /v1/messages API. The system prompt configures Claude as a specialist carbon advisor:

Grounded in real CO₂e data and scientific consensus
Solutions-focused and non-judgmental in tone
Concise by default (3–5 sentences), detailed on request
Maintains conversation history for coherent multi-turn dialogue

Quick-start chips offer common questions. The calculator and dashboard both surface entry points into this module with pre-filled context messages.
Module 4 — Eco Tips
A filterable card grid of 12 high-quality reduction actions across Transport, Home, Food, and Shopping. Each tip includes:

Category tag
Actionable title and evidence-based description
Realistic annual CO₂e saving range
Impact badge (high / medium / low)

Filtering is handled client-side in JavaScript with no additional API calls.
Module 5 — Goals & Progress
Visual progress tracking against four pre-set reduction goals, each tied to a specific behaviour change with a real-world equivalent (e.g. "going car-free every Friday"). Includes:

Progress bars reflecting partial goal completion
A 2030 Paris Agreement alignment tracker showing distance from the 2.5t per-capita target
A "Generate my reduction roadmap" button that opens a pre-filled AI conversation


Assumptions Made

Emission factors are approximate averages; they vary by country, vehicle type, grid mix, and season. The platform uses India-relevant figures where applicable (e.g. India electricity grid: ~0.82 kg CO₂e/kWh → simplified to 0.23 after renewables mix assumption).
Flight emissions are simplified to a flat 0.3t CO₂e per round trip. Real calculations would need origin, destination, and class of travel.
Diet factors are derived from published lifecycle assessment studies (Poore & Nemecek 2018, Oxford Martin School). They represent averages and do not account for regional food systems.
Shopping emissions use a rough 10 kg CO₂e/order heuristic. Actual values depend heavily on product type, origin, and delivery distance.
Dashboard data (8.4t baseline, monthly trend) is illustrative sample data representing a typical urban Indian household. In a production system, this would be sourced from the calculator, connected to smart meters, or imported from bank/card data.
Progress percentages on the Goals page are simulated for demonstration. A production version would track actual logged behaviour over time.
API authentication is handled by the Anthropic Claude.ai platform sandbox — no API key is exposed in client-side code.


Technical Stack
LayerTechnologyUI FrameworkVanilla HTML/CSS/JS (widget-native)ChartsChart.js 4.4.1 (UMD via cdnjs)AI IntegrationAnthropic Claude API (claude-sonnet-4-20250514)IconsTabler Icons (outline webfont)StylingCSS custom properties (design system variables)StateIn-memory JS (no localStorage)

Potential Extensions (Production Roadmap)

Smart meter integration — pull real energy data via MQTT or utility APIs
Bank/card transaction analysis — categorise spending and estimate embodied emissions
Community benchmarking — compare with anonymised local and demographic averages
Offset marketplace — vetted carbon offset projects tied to reduction gaps
Wearable/mobility integration — auto-detect transport mode via GPS
Employer carbon reporting — aggregate employee footprints for Scope 3 reporting
Gamification — streaks, badges, and social challenges for sustained behaviour change
