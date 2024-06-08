# **Weather App**

**The Weather App** is a web application built with Vue.js that enables users to retrieve current weather information and a 4-day forecast for any city worldwide. Leveraging the OpenWeatherMap API, this app provides real-time weather data with a user-friendly interface.

## Features

- **Search Functionality:** Users can search for weather information by entering the name of a city.
- **Current Weather Display:** The app shows current weather details such as temperature, description, humidity, wind speed, and pressure.
- **4-Day Forecast:** Users can view a 4-day weather forecast to plan ahead.
- **Error Handling:** The app gracefully handles errors for invalid city names and provides feedback to users.

## Prerequisites

Before running the Weather App, ensure you have the following installed:

- **Node.js and npm:** Required for package management.
- **OpenWeatherMap API Key:** Obtain an API key to access weather data from the OpenWeatherMap API.

## Getting Started

Follow these steps to set up and run the Weather App locally:

1. **Clone the Repository**:
   git clone https://github.com/Aboagye-Heming/weather-app.git
   cd weather-app

2. **Install Dependencies**:
   npm install

3. **Configure API Key**:
   Create a `.env` file in the root directory and add your OpenWeatherMap API key:
   VUE_APP_WEATHER_API_KEY=your_openweathermap_api_key

4. **Run the App**:
   npm run serve

5. **Access the App**:
   Open your browser and navigate to `http://localhost:8080` to use the Weather App.

## Project Structure

- `src/components/WeatherReport.vue`: Component for displaying current weather details.
- `src/components/DaysWeather.vue`: Component for displaying the 4-day weather forecast.
- `src/App.vue`: Main component containing the search bar and logic for displaying weather details.

## Technologies Used

- **Vue.js:** A progressive JavaScript framework for building user interfaces.
- **Axios:** A promise-based HTTP client for making API requests.
- **Moment.js:** A library for parsing, validating, manipulating, and displaying dates and times.
- **Bootstrap:** A front-end framework for designing responsive and mobile-first websites.
- **OpenWeatherMap API:** Provides access to real-time weather data and forecasts.

## Deployment

You can access the deployed Weather App at https://weather-app-321real-time.netlify.app/.

## Acknowledgements

- Weather data provided by [OpenWeatherMap](https://openweathermap.org/).
- Icons courtesy of [FontAwesome](https://fontawesome.com/).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

**Kwabena Aboagye-Heming**
