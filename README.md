<div align="center">

# 🎧 Logitech Headsets Modded Driver

### Restore 2.0 Stereo to enable Windows Spatial Audio


Most Logitech G headsets (PRO X, G733, G635, etc.) are forced into an 8‑channel (7.1) virtual endpoint by G HUB drivers.<br>This project restores a native 2.0 stereo endpoint so Windows Spatial Audio actually works.

</div>

<br>

## 🚨 The Problem

Most Logitech G headsets (PRO X, G733, G635, etc.) are forced into an 8‑channel (7.1) virtual device by G HUB Drivers, which causes two main issues:

<table width="100%" border="1" cellpadding="16" cellspacing="0">
<tr>
<td width="50%" valign="top">

**🔇 Audio Compression**

The sound feels muffled and compressed due to forced APO limiters.

</td>
<td width="50%" valign="top">

**🚫 Blocked Features**

You cannot enable Dolby Atmos or DTS Sound Unbound because Windows requires a native 2.0 Stereo endpoint.

</td>
</tr>
</table>

<br>

## 🧭 Choose Your Method

There are **two** completely different ways to use this project. Choose the one that suits you:

<table width="100%" border="1" cellpadding="16" cellspacing="0">
<tr>
<td width="50%" valign="top">

### 🛠️ Method 1
**Modify the Official Driver**

Use the official Logitech driver and perform the modification yourself by following the guide.

| | |
|---|---|
| Starting point | **Official Logitech driver** |
| INF editing required | **Yes** |
| Best for | Doing it yourself |

</td>
<td width="50%" valign="top">

### 📦 Method 2
**Ready-to-Install Modded Driver**

Download the already modified and signed driver + certificate and install it directly.

| | |
|---|---|
| Starting point | **Pre-modified, self signed driver** |
| INF editing required | **No** |
| Best for | Just wanting it installed |

</td>
</tr>
</table>

<br>

---

## 🛠️ Method 1 — Modify the Official Driver

### The Modification

After extracting the official Logitech G HUB audio driver, this manual INF‑level modification de‑couples the hardware from the forced surround engine. It strips away the "muffled" virtual 7.1 layer, restoring a high‑fidelity 2.0 output while maintaining full Blue VO!CE compatibility.

Open your `logi_audio.inf` with a text editor and locate your headset's specific section (e.g. `; G735 specific section`), then apply the two steps below.

<br>

<table width="100%" border="1" cellpadding="16" cellspacing="0">
<tr><td>

### 🔧 &nbsp;Step 1 — Remove the Surround Registration

In the `**_HW**` section of your model, find this line:

```ini
(Surround + Name): AddReg=logi_audio_surround.HWAddReg, G735_FriendlyName.AddReg
```

**Remove** the surround part so it looks like this:

```ini
AddReg=G735_FriendlyName.AddReg
```

</td></tr>
</table>

<br>

<table width="100%" border="1" cellpadding="16" cellspacing="0">
<tr><td>

### 🔧 &nbsp;Step 2 — Remove the Surround Service

Locate this block:

```ini
[lgAudio_G735.Services]
Include = wdma_usb.inf
Needs = USBAudio.Services
AddService = logi_audio_surround,,logi_audio_surround_Service_Inst
```

**Remove** the following line:

```diff
- AddService = logi_audio_surround,,logi_audio_surround_Service_Inst
```

<p align="center">
  <img src="img/remove-surround-service.png" alt="Removing the surround service registration" width="450">
  <br>
  <sub>Removing the surround service registration from the INF</sub>
</p>


> Save the changes — you're done for installation.

</td></tr>
</table>

<br>

### 💿 Installation Guide

<table width="100%" border="1" cellpadding="16" cellspacing="0">
<tr><td>

### 🧹 &nbsp;Step 1 — Clean Uninstall

`Device Manager` → Right‑click your headset → `Uninstall Device` → Check **Attempt to remove driver for this device**

</td></tr>
</table>

<br>

<table width="100%" border="1" cellpadding="16" cellspacing="0">
<tr><td>

### 🔐 &nbsp;Step 2 — Disable Driver Signature Enforcement

Restart Windows while holding <kbd>Shift</kbd> → `Troubleshoot` → `Advanced options` → `Startup Settings` → `Restart` → Press <kbd>7</kbd> or <kbd>F7</kbd>

</td></tr>
</table>

<br>

<table width="100%" border="1" cellpadding="16" cellspacing="0">
<tr><td>

### 💿 &nbsp;Step 3 — Manual Driver Update

- Open `Device Manager`
- Right‑click your headset (or USB Audio Device)
- `Update Driver` → `Browse my computer` → `Let me pick from a list` → `Have Disk`
- Point to your modified `logi_audio.inf`
- Ignore the security warning and click **Yes**

</td></tr>
</table>

<br>
<br>
<br>

---

## 📦 Method 2 — Ready-to-Install Modded Driver

> [!NOTE]
> For users who do not want to manually modify the official driver.

The driver provided by this project is already **modified and signed**. No INF editing is required.

1. 📜 Install the provided public certificate.
2. 💿 Install the pre‑modified driver through Device Manager.

> The pre‑modified driver and public certificate are available through **[GitHub Releases](../../releases)**.

<br>

---

## ✅ The Result

<table width="100%" border="1" cellpadding="14" cellspacing="0">
<tr><td>🎧 <b>Spatial Sound</b></td><td>You can now select Dolby Atmos for headphones or DTS Headphone:X directly from Windows settings</td></tr>
<tr><td>🔊 <b>No more G HUB audio compression</b></td><td>You get the raw frequency response of the headset</td></tr>
<tr><td>⚙️ <b>Software Compatibility</b></td><td>G HUB with the latest version still recognizes the device, and Blue VO!CE microphone features remain fully functional</td></tr>
<tr><td>🎙️ <b>Updated Blue VO!CE</b> <i>(pre‑modded driver only)</i></td><td>Devices that already support it get the newer Blue VO!CE 2.0 effect</td></tr>
</table>

> [Note]
> Even after applying this mod, you must go into the G HUB software settings and ensure that **Enable Surround Sound** is unchecked (Off).

### Before vs After

<table border="1" cellpadding="14" cellspacing="0">
<tr>
<td align="center" width="50%">

**BEFORE**<br>Original 7.1 Surround

<img src="img/before-7.1-surround.png" alt="Before - 7.1 Surround configuration" width="380">

</td>
<td align="center" width="50%">

**AFTER**<br>Restored 2.0 Stereo

<img src="img/after-2.0-stereo.png" alt="After - restored 2.0 Stereo configuration" width="380">

</td>
</tr>
</table>

<br>

---

## 🎧 Supported Headsets

`G430` `G431` `G432` `G433` `G533` `G633` `G635` `G733` `G933` `G935` `PRO X` `PRO X Wireless` `PRO X 2`

<br>

<div align="center">
<sub>Community driver modification — not affiliated with or endorsed by Logitech.</sub>
</div>
