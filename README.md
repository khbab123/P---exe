name: Build EXE

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: windows-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'

      - name: Install PyInstaller
        run: pip install pyinstaller

      - name: Build EXE
        run: pyinstaller --onefile main.py

      - name: Upload EXE
        uses: actions/upload-artifact@v3
        with:
          name: output-exe
          path: ./dist/main/main.exe
          
