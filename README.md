import os
import platform
import psutil

def get_system_info():
    print("="*20, "SYSTEM INFO", "="*20)
    print(f"OS: {platform.system()} {platform.release()}")
    print(f"Processor: {platform.processor()}")
    print(f"RAM: {round(psutil.virtual_memory().total / (1024**3), 2)} GB")
    
    print("\n" + "="*20, "RUNNING PROCESSES", "="*20)
    for process in psutil.process_iter(['pid', 'name']):
        try:
            print(f"ID: {process.info['pid']} | Name: {process.info['name']}")
        except (psutil.NoSuchProcess, psutil.AccessDenied):
            pass

if __name__ == "__main__":
    get_system_info()

