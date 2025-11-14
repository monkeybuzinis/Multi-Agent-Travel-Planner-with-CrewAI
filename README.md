# AI-Powered Travel Planning Agentic System

An intelligent multi-agent travel planning system that creates comprehensive, hour-by-hour travel itineraries with integrated flight searches, accommodation recommendations, and local cultural insights.

## Features

- **Smart Multi-City Routing**: Automatically identifies optimal gateway cities and travel routes
- **Integrated Flight Search**: Real-time flight searches with exact arrival/departure times using Google Flights API
- **Dynamic Itinerary Generation**: Creates detailed day-by-day schedules with morning/afternoon/evening breakdowns
- **Hotel Recommendations**: Finds accommodations aligned with your itinerary and budget
- **Local Cultural Insights**: Provides customs, etiquette, food recommendations, and practical tips
- **Budget-Aware Planning**: Tailors recommendations to your specified budget level
- **Personalized Preferences**: Customizes activities based on your interests (culture, food, adventure, etc.)

## System Architecture

The system uses a 3-phase sequential approach:

### Phase 1: Itinerary Planning

- **Destination Researcher**: Researches destinations and identifies gateway cities
- **Attractions Specialist**: Discovers activities and experiences based on preferences
- **City Route Planner**: Plans optimal multi-city routes
- **Preliminary Itinerary Planner**: Creates detailed day-by-day schedules

### Phase 2: Flight Search

- **Flight Specialist**: Searches flights based on identified cities and provides exact timing

### Phase 3: Integration & Finalization

- **Final Itinerary Integrator**: Combines flights with itinerary for perfect timing
- **Accommodation Specialist**: Finds hotels matching the finalized schedule
- **Local Guide**: Provides cultural and practical information
- **Travel Manager**: Compiles everything into a comprehensive travel plan

## Technologies Used

- **CrewAI**: Multi-agent orchestration framework
- **LangChain**: LLM integration and tooling
- **OpenAI GPT-4**: Primary language model
- **Tavily API**: Web search capabilities
- **SerpAPI**: Flight and hotel search via Google Flights/Hotels
- **Python 3.x**: Core programming language

## Prerequisites

- Python 3.8+
- Google Colab account (or local Python environment)
- API Keys for:
  - OpenAI
  - Tavily
  - SerpAPI

##  Installation

### Clone the repository

```bash
git clone https://github.com/yourusername/travel-planning-agent.git
cd travel-planning-agent
```

### Install required packages

```bash
pip install crewai langchain langchain-openai langchain-community python-dotenv google-search-results
```

### Set up API keys

Create a `.env` file or set up secrets in Google Colab:

```env
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
SERPAPI_API_KEY=your_serpapi_api_key
```

##  Usage

### Running in Google Colab

1. Upload the notebook to Google Colab
2. Add your API keys to Colab Secrets:
   - Go to the 🔑 icon in the left sidebar
   - Add `OPENAI_API_KEY`, `TAVILY_API_KEY`, and `SERPAPI_API_KEY`
3. Run all cells

### Running Locally

```python
from travel_planning_system import *

# Set your API keys
os.environ["OPENAI_API_KEY"] = "your_key"
os.environ["TAVILY_API_KEY"] = "your_key"
os.environ["SERPAPI_API_KEY"] = "your_key"

# Create tasks
tasks = create_smart_adaptive_tasks(
    origin_city="San Francisco",
    destination="Thailand",
    travel_dates="2025-03-15 to 2025-03-22",
    duration_days=7,
    preferences="Culture, Food, Temples, Beaches",
    budget="moderate",
    travelers_count=2
)

# Execute
crew = Crew(agents=agents, tasks=tasks, process=Process.sequential)
results = crew.kickoff()
```

##  Input Parameters

When running the system, you'll be prompted for:

- **Departure City**: Your starting location (e.g., "San Francisco")
- **Destination**: Country or city (e.g., "Thailand" or "Bangkok")
- **Travel Dates**: Format: `YYYY-MM-DD` or `YYYY-MM-DD to YYYY-MM-DD`
- **Duration**: Number of days for the trip
- **Number of Travelers**: How many people are traveling
- **Preferences**: Your interests (e.g., "Culture, Food, Adventure")
- **Budget**: Level - `budget`, `moderate`, or `luxury`

## Example Output

The system generates a comprehensive travel plan including:

### 🌍 COMPLETE TRAVEL PLAN

#### ✈️ FLIGHT DETAILS
- Outbound: SFO → BKK on 2025-03-15
  Arrive: 8:30 PM at Suvarnabhumi Airport
- Return: CNX → SFO on 2025-03-22
  Depart: 11:45 AM from Chiang Mai International

#### 📍 DESTINATION OVERVIEW
- Weather, culture, and practical information

#### 🎯 ATTRACTIONS & ACTIVITIES
- Organized by city with timing and costs

#### 🗓️ DETAILED TIME-BASED ITINERARY

**DAY 1 (2025-03-15) - ARRIVAL IN BANGKOK**

FLIGHT ARRIVAL: 8:30 PM at Suvarnabhumi Airport

**Evening (8:30 PM - 11:00 PM):**
- Airport transfer to hotel (45 mins)
- Check-in and rest
- ...

#### 🏨 ACCOMMODATION
- Hotel recommendations with pricing

#### 🧭 LOCAL GUIDE
- Cultural tips and practical information

## 🔧 Key Features Explained

### Intelligent City Resolution
The system automatically identifies that "Thailand" requires routing through specific cities (Bangkok, Chiang Mai) rather than searching for flights to "Thailand" directly.

### IATA Code Detection
Built-in airport code database plus dynamic SerpAPI lookup for less common airports.

### Time Integration
Flight arrival/departure times are integrated into the daily schedule for realistic planning.

### Sequential Processing
Tasks execute in order to ensure later agents have necessary information from earlier agents.

##  Troubleshooting

### Issue: Flight search fails

**Solution**: Verify SerpAPI key is valid and has Google Flights credits

### Issue: No hotels found

**Solution**: Check date format is `YYYY-MM-DD` and destination is correctly spelled

### Issue: Generic itinerary without specific cities

**Solution**: Ensure Phase 1 agents complete before Phase 2 runs

##  Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

##  License

This project is licensed under the MIT License - see the LICENSE file for details.

##  Acknowledgments

- CrewAI for the multi-agent framework
- Anthropic Claude and OpenAI for AI capabilities
- SerpAPI for flight and hotel search functionality
- Tavily for web search capabilities

## Author

**Khanh Le** 




