# Smart_Data_Analyzer
# test_analyzer.py
import sys
import os
import pandas as pd
import matplotlib.pyplot as plt
import traceback

class SmartDataAnalyzer:
    def _init_(self, source):
        # Accept either a file path (str) or a pandas DataFrame
        if isinstance(source, str):
            if not os.path.exists(source):
                raise FileNotFoundError(f"CSV file not found: {source!r}. Current dir: {os.getcwd()}")
            try:
                self.data = pd.read_csv(source)
                print("✅ Data loaded from CSV:", source)
            except Exception as e:
                raise RuntimeError(f"Failed to read CSV {source!r}: {e}")
        elif isinstance(source, pd.DataFrame):
            self.data = source
            print("✅ Data loaded from DataFrame")
        else:
            raise TypeError("source must be a file path (str) or a pandas.DataFrame")

    def overview(self):
        print("\n--- Dataset Overview ---")
        print(self.data.head())
        print("\nShape:", self.data.shape)

    def summary(self):
        print("\n--- Summary Statistics ---")
        print(self.data.describe(include='all'))

    def missing_values(self):
        print("\n--- Missing Values ---")
        print(self.data.isnull().sum())

def run_demo():
    print("Python version:", sys.version.splitlines()[0])
    print("Executable:", sys.executable)
    print("Working dir:", os.getcwd())
    # Warn about common pitfalls
    script_name = os.path.basename(_file_)
    if script_name.lower().startswith(("pandas", "matplotlib")):
        print("⚠ Warning: Your script filename starts with 'pandas' or 'matplotlib' — rename the file (e.g. test_analyzer.py) to avoid import conflicts.")

    try:
        # Replace this with: analyzer = SmartDataAnalyzer("yourfile.csv") to load your CSV
        df = pd.DataFrame({
            "Name": ["A", "B", "C", "D"],
            "Marks": [85, 90, 78, 92],
            "Age": [20, 21, 19, 22]
        })

        analyzer = SmartDataAnalyzer(df)
        print("analyzer object:", analyzer)

        analyzer.overview()

        try:
            analyzer.summary()
        except Exception as e:
            print("\n⚠ Error inside summary():", e)
            traceback.print_exc()

        try:
            analyzer.missing_values()
        except Exception as e:
            print("\n⚠ Error inside missing_values():", e)
            traceback.print_exc()

    except Exception:
        print("\n🔥 Unhandled exception during run:")
        traceback.print_exc()
        print("\nPlease copy-paste the full traceback above here so I can diagnose.")

if __file__ == "__main__":
    run_demo()
