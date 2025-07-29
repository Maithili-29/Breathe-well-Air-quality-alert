# Breathe-well-Air-quality-alert
import argparse
import logging
from breathe_well.api import fetch_air_quality, AirQualityAPIError
from breathe_well.utils import format_air_quality
from breathe_well.config import DEFAULT_CITY

logging.basicConfig(level=logging.INFO)

def main():
    parser = argparse.ArgumentParser(description="Breathe Well Air Quality CLI")
    parser.add_argument("--city", type=str, default=DEFAULT_CITY, help="City name to query air quality")
    args = parser.parse_args()

    try:
        data = fetch_air_quality(args.city)
        if data:
            print(format_air_quality(data))
        else:
            print(f"No air quality data available for city: {args.city}")
    except AirQualityAPIError as e:
        print(f"Error: {e}")

if __name__ == "__main__":
    main()
