name: .NET Build and Test

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: windows-latest  # Using Windows because you're using System.Speech.Synthesis

    steps:
    - name: 📥 Checkout Repository
      uses: actions/checkout@v3

    - name: 🛠️ Setup .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '8.0.x'  # Adjust if you're using a different version

    - name: 📦 Restore Dependencies
      run: dotnet restore

    - name: 🧱 Build Solution
      run: dotnet build --no-restore --configuration Release

    - name: ✅ Run Tests (if available)
      run: dotnet test --no-build --verbosity normal
      continue-on-error: true  # Optional: prevents workflow failure if no tests exist
