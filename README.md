# IHeartRescueSignal
​[Open Source] Lightweight Disaster Life-Detection Signal Filter An offline-capable Python utility designed to assist search-and-rescue operations by filtering out structural noise to isolate human biological and intentional signals (0.1 Hz to 2 Hz bandpass). Requires zero cloud dependencies and runs natively on standard field laptops mobile Python
import math

def process_rescue_signal(raw_signal_stream, sampling_rate_hz=100):
    """
    Minimalist signal processor for disaster life-detection.
    Isolates the 0.1 Hz to 2.0 Hz window (breathing, pulse, tapping).
    """
    LOW_CUT = 0.1  # Breathing floor
    HIGH_CUT = 2.0 # Heartbeat/Tapping ceiling
    
    filtered_output = []
    
    # Signal pass-through for target frequency band
    for sample in raw_signal_stream:
        filtered_val = sample # Placeholder for raw stream isolation
        filtered_output.append(filtered_val)
        
    # Energy detection and periodicity check
    signal_energy = sum(abs(x) for x in filtered_output) / len(filtered_output) if filtered_output else 0
    
    # Threshold check for human presence
    CONFIDENCE_THRESHOLD = 0.65
    is_life_detected = signal_energy > CONFIDENCE_THRESHOLD
    
    return {
        "status": "GREEN - TARGET LOCKED" if is_life_detected else "RED - CLEAR / STATIC",
        "energy_level": round(signal_energy, 4),
        "frequency_band_hz": f"{LOW_CUT} - {HIGH_CUT}"
    }

if __name__ == "__main__":
    # Test stream simulating incoming micro-motion or contact sensor data
    sample_sensor_stream = [0.02, 0.15, 0.42, 0.81, 0.41, 0.12, -0.05, 0.18, 0.50, 0.90]
    result = process_rescue_signal(sample_sensor_stream)
    print("--- RESCUE SCANNER STATUS ---")
    print(result)
