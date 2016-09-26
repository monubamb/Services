FROM microsoft/dotnet:1.0.0-core

# Set the Working Directory
WORKDIR /app

# Configure the listening port to 8088
ENV ASPNETCORE_URLS http://*:8088
EXPOSE 8088

# Copy the app
COPY . /app

# Start the app
ENTRYPOINT dotnet WebApplication2.dll
