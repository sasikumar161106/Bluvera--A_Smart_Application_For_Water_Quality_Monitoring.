# Bluvera - A Smart Application For Water Quality Monitoring

Welcome to Bluvera, a sophisticated and smart application engineered for the real-time monitoring and comprehensive analysis of water quality. This project aims to enhance water safety and management by integrating advanced IoT sensor data with environmental insights, providing users with actionable information through an intuitive mobile interface.

## Project Overview

Bluvera is designed to be a central hub for understanding water conditions. Leveraging IoT technology, it connects with smart sensors to gather critical water parameters in real-time. Beyond just water quality, the application intelligently incorporates relevant weather data, offering a holistic perspective on environmental factors that influence water health. Built with Flutter, Bluvera delivers a seamless cross-platform experience, prioritizing user convenience and security through features like biometric authentication. It caters to a range of applications, from agricultural management to environmental protection and ensuring potable water safety.

## Features

Bluvera offers a robust set of features to provide comprehensive water quality insights:

*   **Real-Time Water Quality Monitoring**: Connects with smart sensors to continuously track and display essential water quality metrics such as pH, turbidity, temperature, dissolved oxygen, and more.
*   **Integrated Weather Data**: Provides contextual understanding by incorporating local or relevant weather information alongside water quality data, helping users identify correlations and predict trends.
*   **Data Visualization**: Presents water quality data through interactive dashboards and charts, making complex information easy to understand and analyze over time.
*   **Alerts & Notifications**: Notifies users with automated alerts when monitored water quality parameters deviate from predefined safe thresholds, enabling prompt intervention.
*   **Historical Data Tracking**: Stores and allows analysis of past water quality data, facilitating trend identification, seasonal variation analysis, and long-term environmental planning.
*   **Secure Biometric Authentication**: Enhances user security and accessibility by implementing biometric login capabilities (e.g., fingerprint, face unlock) for secure access to the application.
*   **Cross-Platform Mobile Application**: Developed using Flutter, ensuring a consistent, high-performance, and visually appealing user experience across Android and potentially iOS devices, with extensibility to other platforms.
*   **Custom Android Experience**: Includes a customized Android splash screen and application icon, providing a branded and polished look and feel from the moment the app launches.

## Technology Stack

*   **Frontend Framework**: Flutter (using Dart language)
*   **Platform**: Android (with support for iOS, Web, Desktop platforms implied by Flutter metadata)
*   **Core Concepts**: Internet of Things (IoT) Integration, Data Analytics, Biometric Security
*   **Build System**: Gradle (for Android)

## Project Structure

This project follows a standard Flutter application structure with platform-specific configurations:

*   `.gitignore`: Standard Git ignore file for Flutter projects, covering build artifacts, caches, and IDE-specific files.
*   `.metadata`: Flutter-specific metadata file, tracking project type, Flutter version, and migration details across various platforms (Android, iOS, Web, Desktop).
*   `analysis_options.yaml`: Configuration for the Dart analyzer, enforcing code quality and style conventions using `flutter_lints`.
*   `android/`: Contains platform-specific configurations and source code for the Android application.
    *   `app/src/debug/AndroidManifest.xml`: Android manifest for debug builds, primarily granting `INTERNET` permission for development tools.
    *   `app/src/main/AndroidManifest.xml`: The primary Android manifest, declaring the application name (`Bluvera`), icon, core activity, and essential permissions such as `USE_BIOMETRIC` and `USE_FINGERPRINT`. It also configures the custom splash screen theme.
    *   `app/src/main/kotlin/com/example/smart_water_quality_app/MainActivity.kt`: The main entry point for the Flutter application on Android, extending `FlutterFragmentActivity`.
    *   `app/src/main/res/`: Android resource directories, including:
        *   `drawable-v21/launch_background.xml` & `drawable/launch_background.xml`: XML files defining the application's splash screen background.
        *   `mipmap-anydpi-v26/ic_launcher.xml`: Adaptive launcher icon definition.
        *   `values-night/styles.xml` & `values/styles.xml`: XML files for defining themes and styles, including `LaunchTheme` for the splash screen and `NormalTheme` for the main application window, supporting both light and dark modes.
        *   `values/colors.xml`: Defines custom colors, such as the background color for the launcher icon (`ic_launcher_background`).
*   `lib/`: (Inferred) This directory is where the main Dart source code for the Flutter application resides, including `main.dart` and other components that implement the application's logic and UI.
*   `LICENSE`: Details the project's licensing information (MIT License).
*   `README.md`: The primary documentation file for the project (this document).

### Note on `DOCSYNC.md`

The `DOCSYNC.md` file found in this repository appears to be documentation for an unrelated project titled "DocSync," described as an "AI-powered technical documentation agent." While some content from this file pertains to "Bluvera," the primary focus of that document is on a different system. Its inclusion here is likely accidental or a remnant from a previous context. This `README.md` focuses exclusively on the Bluvera application.

## Setup and Usage

To set up and run the Bluvera application locally, follow these instructions.

### Prerequisites

*   **Flutter SDK**: Ensure you have Flutter installed (version `3.x` or higher is recommended).
    *   [Install Flutter](https://flutter.dev/docs/get-started/install)
*   **Android Studio** or **VS Code**: With the Flutter and Dart plugins installed.
*   **Git**: For cloning the repository.
*   **Android Device or Emulator**: Required to run the application.

### Installation

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/sasikumar161106/Bluvera--A_Smart_Application_For_Water_Quality_Monitoring.git
    cd Bluvera--A_Smart_Application_For_Water_Quality_Monitoring
    ```

2.  **Get Flutter dependencies**:
    ```bash
    flutter pub get
    ```

3.  **Run the application**:
    Ensure you have an Android emulator running or a physical Android device connected and recognized by Flutter (`flutter devices`).
    ```bash
    flutter run
    ```
    This command will build the application and deploy it to your selected device or emulator.

### Biometric Authentication

The application is configured to request necessary biometric permissions (`USE_BIOMETRIC`, `USE_FINGERPRINT`). To test the biometric authentication feature, ensure your Android device or emulator is set up with fingerprint or other biometric security methods.

### IoT Integration and Weather Data Configuration

The specifics for connecting to IoT sensors or configuring external weather data sources are implemented within the Dart code in the `lib/` directory. Developers looking to integrate specific hardware or APIs will need to modify or extend the existing application logic to interface with their chosen IoT devices, cloud platforms, or weather data providers.

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page for current needs or to propose new features.

## License

This project is licensed under the [MIT License](LICENSE).

Copyright (c) 2026 SASIKUMAR S.