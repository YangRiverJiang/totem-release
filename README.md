# Totem

Totem is experimental smartphone GNSS positioning software for Android. This
repository contains the current Totem APK release, user manual, and release
checksums.

## Download

- APK: [totem-release-jul22-2026.apk](totem-release-jul22-2026.apk)
- User manual: [docs/Totem_User_Manual.pdf](docs/Totem_User_Manual.pdf)
- Build date: Jul22-2026
- Release date: July 22, 2026
- App version: 2026.07.22-guest
- Android package: `com.sleepy.totem.guest`
- Source commit: `8cb26bb`
- SHA-256: `B28FE199ABE0E983EF5D01E07477FC5233D57C417C626D48B96A6BDEBC03D6D3`

## APK Changelog

### 2026.07.22-guest

- Updated the default broadcast ephemeris endpoint to the Jul22 validation
  stream at `70.72.235.104:17003`.
- Added build-variant map key routing so debug builds and release builds use
  separate Google/AMap API keys.
- Updated release metadata, checksum, and source alignment for commit
  `8cb26bb`.

### 2026.07.17-guest

- Fixed replay and post-process preparation for exported Totem datasets,
  including packages that contain masked internal files.
- Added a fallback export path when Android cannot create a Downloads entry, so
  users can still share the generated package.
- Improved AMap coordinate alignment by applying WGS-84 and GCJ-02 conversion
  for map markers, camera state, tracks, and overlays.
- Persisted engine options so replay and post-process pages can reuse the
  latest app-side processing settings more reliably.
- Corrected the Android package version name to `2026.07.17-guest`.
- Updated release metadata, checksum, and user manual for the Jul17-2026 APK.

## Install

Install with ADB:

```powershell
adb install -r totem-release-jul22-2026.apk
```

Or copy the APK to an Android phone and open it from the system file manager.
If Android blocks installation, enable installation from the current source in
system settings and retry.

## Device Requirements

- Android device with raw GNSS measurement support.
- Android 10 or newer is recommended.
- Location permission must be allowed while using the app. It is recommended to enable the "Force full GNSS measurements" option in the Android "Developer options" menu.
- Internet access is required for online maps, broadcast ephemeris streams, and
  network correction streams.

## First Run

1. Open Totem.
2. Grant location permission when Android asks for it.
3. If Google Maps is unavailable on the device, switch the map provider to AMap
   or OSM from the map selector.
4. Wait outdoors until the phone GNSS marker appears on the Map page.

## Configure Processing Before Solving

Open Options before starting a field session and select the processing mode:

- SPP: Standard point positioning. Broadcast ephemeris is required. Network
  correction streams are not required.
- SPK: Standard point kinematic positioning. Network correction streams are not
  required, but broadcast ephemeris is required.
- RTK: rover-base relative positioning. Configure broadcast ephemeris and the
  correction/base stream first.
- DSPP: differential SPP. Configure broadcast ephemeris and the correction/base
  stream first.

The Control page can collect measurements without solving. To produce live
Totem solutions, configure the mode, broadcast ephemeris, and any required
correction streams, then press Collect and then Solve.
Note that for each of the broadcast ephemeris and correction streams, Totem applies a TCP client to connect to the server IP address.

## Collect Data

1. Open the Control page.
2. Check Battery, Memory, Temperature, Measurements, Solutions, Failure Rate,
   and Duration.
3. Press Collect to record phone GNSS measurements.
4. Press Solve if live positioning is needed.
5. Keep the app open during the field session.
6. Stop Solve first if it is running, then stop Collect when the session is
   complete.

For replay, every mode needs phone measurements and broadcast ephemeris data.
For RTK and DSPP replay, the dataset must also include correction/base data.
Collect with Solve enabled and the required streams configured if you want
post-process replay later.

## Export Data

1. Open Export.
2. Select a logged dataset.
3. Export the dataset package.
4. Share or copy the ZIP file as needed.

Measurement text files and solution files are kept readable. Internal
diagnostic files may use a binary masking format.

## Replay And Post-process

1. Configure Options for the desired replay mode.
2. Open post-process or replay.
3. Select a dataset recorded by Totem.
4. Press Process or Solve, depending on the page.
5. Wait for the completion message, then export results if needed.

Replay uses the current Options. If the dataset does not contain broadcast
ephemeris data, Totem cannot replay any processing mode. If the selected mode is
RTK or DSPP but the dataset does not contain correction/base data, Totem will
stop before launching the engine and ask you to switch to SPP/SPK or use a
complete dataset.

## Main Pages

- Map: phone position, Totem solution position, map provider, legend, recenter,
  and zoom controls.
- Control: measurement collection, solving, session counters, export, and
  compact console messages.
- Solution: current solution, timing, position, accuracy, geometry, and motion.
- Satellites: skyplot and satellite signal list.

## Troubleshooting

- No map: switch map provider, check network access, or move to an area with
  available map data.
- No phone position: confirm location permission and move outdoors.
- No Totem solution: confirm Solve is enabled, broadcast ephemeris is available,
  and the selected mode has any required correction stream.
- RTK or DSPP replay is blocked: use a dataset collected with Solve and
  broadcast ephemeris plus correction/base streams, or switch replay mode to
  SPP/SPK when correction/base data is unavailable.
- Export fails: check available storage and retry after closing other apps.
- Unsupported device: the phone may not expose Android raw GNSS measurements
  required by Totem.

## Publications

- Author profile: [Yang Jiang on Google Scholar](https://scholar.google.ca/citations?user=vfQfXkMAAAAJ&hl=en)
- Thesis: Yang Jiang, [High-accuracy Smartphone RTK Positioning: Major
  Challenges and Innovative Solutions](https://ucalgary.scholaris.ca/items/31d85cbd-6270-4948-8a76-007c54df7d70),
  PhD thesis, University of Calgary, 2025.

## Repository Files

- `totem-release-jul22-2026.apk`: installable Android release APK.
- `docs/`: Totem user manual in PDF and Word formats.
- `media/totem-demo-placeholder.gif`: placeholder for a future usage GIF.
- `checksums.sha256`: APK checksum record.
- `LICENSE`: release license notice.

## Use Notice

Totem is an experimental smartphone GNSS positioning software. Results depend on
device hardware, Android raw GNSS behavior, satellite visibility, correction
availability, and the surrounding signal environment. Do not use this preview
build for safety-critical navigation.

