FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build 

#Set the working directory 
WORKDIR /app 
# Copy the project file and restore dependencies 
COPY *.csproj ./
RUN dotnet restore 
#Copy the rest of the application code 
COPY . ./
# Build the application 
RUN dotnet publish -c Release -o out 
# Use the official .NET 8 runtime image as the base runt 
FROM mcr.microsoft.com/dotnet/aspnet:8.0 

WORKDIR /app

COPY --from=build /app/out .
EXPOSE 8080
ENTRYPOINT ["dotnet", "api.dll"]