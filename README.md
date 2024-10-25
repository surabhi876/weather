# weatherimport requests

# Configuration
API_KEY = '08496cb34a4e5d86910c05ffe430276d'  # Yahaan apni OpenWeatherMap API key daaliye
BASE_URL = 'http://api.openweathermap.org/data/2.5/weather'

# Function to fetch weather data for a city
def get_weather_data(city):
    try:
        # API request URL with city and API key
        url = f"{BASE_URL}?q={city}&appid={API_KEY}"
        response = requests.get(url)
        
        # Check if the response is valid
        if response.status_code == 200:
            data = response.json()
            
            # Convert temperature from Kelvin to Celsius
            temp_kelvin = data['main']['temp']
            temp_celsius = temp_kelvin - 273.15
            
            # Extract important weather information
            weather_condition = data['weather'][0]['main']
            feels_like = data['main']['feels_like'] - 273.15
            city_name = data['name']
            
            # Print the weather information
            print(f"Weather in {city_name}:")
            print(f"Temperature: {temp_celsius:.2f}°C")
            print(f"Feels like: {feels_like:.2f}°C")
            print(f"Condition: {weather_condition}")
        else:
            print(f"Failed to get data for {city}. HTTP Status code: {response.status_code}")
    
    except Exception as e:
        print(f"Error fetching data: {e}")

# User input for city name
city = input("Enter city name: ")
get_weather_data(city)
