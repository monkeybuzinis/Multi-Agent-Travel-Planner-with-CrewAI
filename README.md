# Multi-Agent Travel Planner with CrewAI

An advanced AI-powered travel planning system that uses multiple specialized agents working collaboratively to create comprehensive, personalized travel plans. The system integrates real-time flight search, hotel booking, destination research, and itinerary planning into a seamless multi-agent workflow.

## Overview

This project enhances a travel planning agentic system by adding **real-time flight search** and **hotel search** capabilities using CrewAI's multi-agent framework. The system employs specialized AI agents that work together autonomously to research destinations, plan routes, search for flights and hotels, and compile everything into a detailed, time-integrated travel guide.

## Key Features

- 🤖 **Multi-Agent Architecture**: Specialized agents collaborate to handle different aspects of travel planning
- ✈️ **Real-Time Flight Search**: Integrated SerpAPI Google Flights for live flight data with pricing and schedules
- 🏨 **Hotel Search**: Real-time hotel availability and pricing via SerpAPI Google Hotels
- 🌐 **Web Research**: Tavily search for up-to-date destination information
- 🗺️ **Smart Itinerary Planning**: Two-phase approach that first plans routes, then searches flights
- 🎯 **IATA Code Resolution**: Automatic conversion of city names to airport codes
- ⏰ **Time Integration**: Seamless integration of flight times into day-by-day itineraries

## Architecture

### Multi-Agent System

The system uses **CrewAI** to coordinate multiple specialized agents:

#### Phase 1: Itinerary Planning Agents

1. **Destination Research Expert**
   - Researches comprehensive destination information
   - Identifies main gateway cities for international travel
   - Provides weather, culture, safety, and practical information

2. **Attractions & Activities Expert**
   - Discovers best attractions and activities
   - Recommends experiences based on traveler preferences
   - Finds both popular attractions and hidden gems

3. **City Route Planning Specialist**
   - Plans optimal routes between cities
   - Identifies best arrival and departure cities for flights
   - Determines efficient multi-city routing

4. **Preliminary Itinerary Planner**
   - Creates detailed day-by-day itineraries
   - Identifies specific cities and timing
   - Clearly marks arrival and departure cities for flight booking

#### Phase 2: Flight & Accommodation Agents

5. **Flight Search Specialist**
   - Searches for flights based on itinerary cities
   - Converts city names to IATA airport codes
   - Provides exact arrival and departure times
   - Finds best flight options with pricing

6. **Accommodation Expert**
   - Searches hotels based on itinerary and budget
   - Matches accommodations to traveler preferences
   - Provides pricing, ratings, and amenities

#### Phase 3: Integration Agents

7. **Master Itinerary Integrator**
   - Combines preliminary itinerary with flight information
   - Creates time-integrated schedule with exact flight times
   - Ensures perfect hour-by-hour timing

8. **Local Culture & Practical Guide**
   - Provides essential local knowledge
   - Covers customs, etiquette, food, transportation
   - Offers practical travel tips

9. **Travel Project Manager**
   - Compiles all information into final travel guide
   - Creates polished, comprehensive travel plan
   - Ensures perfect timing integration

## Tools & APIs

### Custom Tools

1. **Web Search Tool** (Tavily)
   - Searches the web for up-to-date destination information
   - Returns formatted results with sources

2. **Find Airport Code Tool** (SerpAPI)
   - Converts city/location names to IATA airport codes
   - Uses Google Search knowledge graph for accurate resolution
   - Handles country names, city names, and location descriptions

3. **Search Flights Tool** (SerpAPI Google Flights)
   - Searches for detailed flight information
   - Provides pricing, duration, stops, airlines
   - Includes specific arrival and departure times
   - Supports both one-way and round-trip flights

4. **Search Hotels Tool** (SerpAPI Google Hotels)
   - Searches hotel options based on destination and dates
   - Provides pricing, ratings, reviews, amenities
   - Matches hotels to itinerary and budget

## Two-Phase Approach

### The Challenge

SerpAPI's Google Flights requires precise IATA airport codes (e.g., "BKK" not "Bangkok"), but users typically provide destinations as countries or city names.

### The Solution

**Phase 1: Itinerary-First Approach**
- Create complete preliminary itinerary first
- Identify optimal arrival gateway city (e.g., Bangkok for Thailand)
- Determine best departure gateway city (e.g., Chiang Mai for northern route)
- Plan logical city-to-city routing

**Phase 2: Flight Search**
- Use itinerary-identified cities
- Convert city names to IATA codes using `find_airport_code` tool
- Search flights with precise airport codes
- Integrate flight times into final itinerary

## Requirements

### Python Packages

```bash
pip install crewai langchain langchain-openai langchain-community python-dotenv google-search-results
```

### Key Libraries
- **CrewAI**: Multi-agent orchestration framework
- **LangChain**: LLM integration and tooling
- **OpenAI**: GPT-4o for agent reasoning
- **SerpAPI**: Real-time flight and hotel search
- **Tavily**: Web search for destination research

### API Keys Required

1. **OpenAI API Key**: For LLM-powered agents
   - Get from: https://platform.openai.com/api-keys

2. **Tavily API Key**: For web search
   - Get from: https://tavily.com/

3. **SerpAPI Key**: For flight and hotel search
   - Get from: https://serpapi.com/

### Setup

1. Create a `.env` file or set environment variables:
   ```bash
   OPENAI_API_KEY=your_openai_key
   TAVILY_API_KEY=your_tavily_key
   SERPAPI_API_KEY=your_serpapi_key
   ```

2. Or in Google Colab, use `userdata`:
   ```python
   from google.colab import userdata
   OPENAI_API_KEY = userdata.get("OPENAI_API_KEY")
   TAVILY_API_KEY = userdata.get("TAVILY_API_KEY")
   SERPAPI_API_KEY = userdata.get("SERPAPI_API_KEY")
   ```

## Usage

1. **Open the Jupyter Notebook**:
   ```bash
   jupyter notebook Multi-Agent-Travel-Planner-with-CrewAI.ipynb
   ```

2. **Set up API keys** (see Requirements section)

3. **Run the notebook cells** to:
   - Install dependencies
   - Initialize agents and tools
   - Create and execute the travel planning crew
   - Generate comprehensive travel plans

### Example Input

```python
origin_city = "New York"
destination = "Thailand"
travel_dates = "2025-06-01 to 2025-06-15"
duration_days = 14
preferences = "Cultural sites, beaches, local food"
budget = "moderate"
travelers_count = 2
```

## Project Structure

```
multi-agent-travel-planner-with-CrewAI/
├── Multi-Agent-Travel-Planner-with-CrewAI.ipynb
└── README.md
```

## How It Works

1. **User Input**: Provides destination, dates, preferences, budget, and traveler count

2. **Phase 1 - Itinerary Planning**:
   - Destination Research Expert gathers comprehensive information
   - Attractions Specialist finds activities matching preferences
   - City Route Planner determines optimal routing
   - Preliminary Itinerary Planner creates day-by-day plan with specific cities

3. **Phase 2 - Flight & Hotel Search**:
   - Flight Search Specialist converts cities to IATA codes
   - Searches real-time flights with exact timing
   - Accommodation Expert finds hotels matching itinerary

4. **Phase 3 - Integration**:
   - Master Itinerary Integrator combines all information
   - Local Guide adds cultural and practical tips
   - Travel Project Manager compiles final comprehensive guide

5. **Output**: Complete travel plan with:
   - Day-by-day itinerary with exact timing
   - Flight options with prices and schedules
   - Hotel recommendations with ratings
   - Local tips and cultural information

## Agent Collaboration

CrewAI coordinates agents using:
- **Memory**: Agents remember previous interactions
- **Task Dependencies**: Tasks are sequenced logically
- **Tool Sharing**: Agents use appropriate tools for their roles
- **Autonomous Coordination**: CrewAI manages agent communication

## Benefits

- ✅ **Comprehensive Planning**: All aspects of travel in one system
- ✅ **Real-Time Data**: Live flight and hotel availability
- ✅ **Personalized**: Adapts to user preferences and budget
- ✅ **Time-Accurate**: Integrates exact flight times into itinerary
- ✅ **Scalable**: Easy to add new agents or tools
- ✅ **Autonomous**: Agents work together without manual intervention

## Limitations

- Requires API keys for external services (costs may apply)
- Flight and hotel search depends on SerpAPI availability
- Processing time depends on number of agents and complexity
- Results quality depends on LLM performance and API data accuracy

## Future Enhancements

- Add weather forecast integration
- Include restaurant recommendations
- Add transportation booking (trains, buses)
- Integrate currency conversion
- Add travel document requirements
- Include travel insurance recommendations

## References

- [CrewAI Documentation](https://docs.crewai.com/)
- [LangChain Documentation](https://python.langchain.com/)
- [SerpAPI Documentation](https://serpapi.com/)
- [Tavily Search API](https://tavily.com/)

## Author

**Khanh Le**



## License

This project uses various third-party APIs. Please refer to their respective terms of service:
- OpenAI API Terms
- SerpAPI Terms
- Tavily Terms

