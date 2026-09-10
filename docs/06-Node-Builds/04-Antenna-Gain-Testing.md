# Antenna Gain Testing

**Objective:** A step-by-step method of procedure (MOP) to verify the true relative gain of an unknown antenna.

**Required Equipment:**
*   **Radios:** 2x duplicate radios running the newest Meshcore version 1.17.1 using the Canada/US preset
> **📝 Note:** Turn off the repeater LNA **set radio.fem.rxgain off**. Set transmit power on the companion to 5dBm

> **⚠️ Warning** The Heltec v4.2 cannot be used for this test because the LNA cannot be disabled. The LNA will skew the results.
*   **Reference Antennas:** 2x Alfa 915 or Alfa 915 clone antennas (Dipole gain = 2.15 dBi)
*   **Analyzer:** 1x NanoVNA with calibration kit (Open, Short, Load) or equivalent
*   **Accessories:** 2x Duplicate pigtails, 2x sturdy mount locations exactly 50ft apart

---

> ⚠️ **CRITICAL HARDWARE PROTECTION WARNING**

> **Never power on or transmit without an antenna securely attached.** Transmitting without an antenna will damage the onboard SX1262 power amplifier chip. Always ensure the antenna is fully screwed onto the pigtail before applying power.

---

## Step 1: Verify Antennas

Before attaching any unknown antenna to a radio, you must verify it's match. A bad match will return some or all of the transmitted power back into the radio, potentially damaging it. Ensure that all antennas are tested and verified.

1. Turn on the NanoVNA.
2. Set the frequency span for the US/Canada 915 MHz band:
   * Navigate to **STIMULUS > START > 900 MHz**.
   * Navigate to **STIMULUS > STOP > 930 MHz**.
3. Attach a pigtail cable to **Port 1 (CH0)** of the NanoVNA.
4. Perform a 1-port calibration using the screw-on brass calibration pieces on the far end of the pigtail:
   * Tap **CAL > CALIBRATE**.
   * Attach the **OPEN** piece, tap OPEN.
   * Attach the **SHORT** piece, tap SHORT.
   * Attach the **LOAD** piece, tap LOAD.
   * Tap **DONE > SAVE 0**.
5. Set the display format to SWR by tapping **DISPLAY > TRACE 0 > FORMAT > SWR**.
6. Remove the calibration load and screw the **Unknown Antenna** onto the pigtail.
7. Tap **MARKER > SELECT MARKER 1** and move it to exactly **910 MHz**.

**✅ Verification Check:** Read the value at 910 MHz. Ensure it reads **1.5:1** or lower before attaching it to a radio.

**⚠️ Warning:** A value above **2.0:1** indicates a severe mismatch that could damage your hardware. Do not proceed with testing if SWR > 2.0.

---

## Step 2: Set Up Outdoor Test Link

1. Measure exactly **50 feet** between two outdoor stations. Ensure the path has a clear, unobstructed line of sight between the two locations. Ensure the area in between the test locations is wide open.
2. Designate Station 1 for the **Companion** radio and Station 2 for the **Repeater** radio.
3. Mount the antennas vertically at both stations at **exactly 3 feet** from the ground. Use metallic supports such as metal stakes or metal poles. Ensure that the antennas to test are mounted on a sturdy mount point.
4. Connect one reference **Alfa 915 antenna** to each radio using identical pigtails.

**📝 Note:** Ensure that both antennas are mounted eaxtly the same way. Omnidirectional antennas must be both pointed **perfectly** upward. Elements of a yagi must point perfectly up/down.

**✅ Verification Check:** Power on both nodes after antennas are attached. Verify that the Companion can successfully connect to the Repeater.

---

## Step 3: Record Control Baseline

1. On the **Companion**, navigate to the node in the contact list and log in to the **Repeater**.
2. Press the **Request Status** button.
3. Wait for the status to load, then locate and record the **Last RSSI** (Received Signal Strength Indicator, measured in dBm).
4. Press **Request Status** 5 times in total, waiting 10 seconds between each request to allow the radios to settle.
5. Write down each reading.
6. Average the 5 readings to establish your **Alfa Antenna** baseline signal.
   * Average = (RSSI_1 + RSSI_2 + RSSI_3 + RSSI_4 + RSSI_51) / 5

**✅ Verification Check:** Check that the 5 recorded "Last RSSI" readings remain stable within ±2 dBm.

---

## Step 4: Measure Unknown Antenna Signal

1. **Turn off the Repeater radio completely.**
2. Unscrew the reference Alfa 915 antenna from the Repeater and attach the **Antenna to Test**.
   * **⚠️ Verification:** Ensure it is vertically oriented and mounted at exactly 3 feet from the ground. Use the exact same pigtail and do not move the stake's location.
3. Power the Repeater back on.
4. From the **Companion** radio, log in to the Repeater again.
5. Press **Request Status** and record the new **Last RSSI**.
6. Write down each reading.
7. Average the 5 readings to establish your **Antenna to Test** baseline signal.
   * Average = (RSSI_1 + RSSI_2 + RSSI_3 + RSSI_4 + RSSI_51) / 5

---

## Step 5: Calculate the True Gain

1. **Calculate the Signal Difference Delta:**
   Subtract the **Alfa Antenna** average from the **Antenna to Test** antenna average.
   > Delta = **Antenna to Test** - **Alfa Antenna**

2. **Calculate True Gain:**
   Add the Delta to the known gain of the Alfa 915 Antenna (2.15 dBi).
   > **Gain** = 2.15 + **Antenna to Test**

**✅ Verification Check (Example):**
If your **Antenna to Test** averaged -58 dBm and the **Alfa Antenna** averaged -65 dBm, the Delta is +7 dB.
Adding this to the 2.15 dBi reference gain yields an estimated true gain of **9.15 dBi** for the **Antenna to Test**.

---

## Appendix: Field Data Logging Sheet

| Test | [ A ] - Alfa 915 Antenna - RSSI | [ B ] - Antenna to Test - RSSI |
| :--- | :--- | :--- |
| **Test 1** | |
| **Test 2** | |
| **Test 3** | |
| **Test 4** | |
| **Test 5** | |
| **AVERAGE** | |

**Final Calculation:**
2.15 + ( [ B ] - [ A ] ) = **________ dBi True Gain**
