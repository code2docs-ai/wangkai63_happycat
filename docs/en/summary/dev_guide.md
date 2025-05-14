[Go to Homepage](../README.md)



## Project Structure

```text
happycat/
├── AndroidManifest.xml  # Application manifest file (Android standard)
├── project.properties   # Project configuration file (Eclipse ADT)
├── proguard-project.txt # ProGuard configuration
├── ic_launcher-web.png  # Web version app icon
├── .project            # Eclipse project file
├── README.md           # Project documentation
├── .classpath          # Eclipse classpath configuration
├── gen/                # Auto-generated files directory (R.java, etc.)
│   └── com/example/happucat/
│       ├── R.java         # Resource ID mapping
│       └── BuildConfig.java # Build configuration
├── .settings/          # IDE configuration directory (Eclipse)
│   ├── org.eclipse.jdt.core.prefs
│   └── org.eclipse.core.resources.prefs
├── res/                # Resource files directory (Android standard)
│   ├── layout/         # Layout files (50+ business pages included)
│   ├── values-*/       # Multi-dimensional resource adaptation (v14/sw600dp, etc.)
│   ├── drawable-*/     # Multi-resolution image resources (hdpi/xhdpi, etc.)
│   ├── menu/           # Menu definition files
│   ├── anim/           # Animation resources
│   └── color/          # Color definitions
├── bin/                # Compilation output directory (Eclipse)
│   ├── classes/        # Compiled Java classes
│   └── res/            # Processed resource files
├── src/                # Source code directory
│   ├── cn/sharesdk/    # Social sharing SDK integration
│   ├── image/          # Image loading module
│   └── com/happycat/   # Main business code
│       ├── activities/    # Activity pages (no clear layering)
│       ├── adapter/       # List adapters
│       ├── Bean/          # Data models
│       └── util/          # Utility classes
├── assets/             # Raw resource files (ShareSDK configuration)
└── libs/               # Third-party libraries
    ├── *.jar           # Dependency libraries (ShareSDK/gson, etc.)
    └── armeabi/        # SO library directory

Naming conventions:
- Lowercase snake case naming (e.g., activity_my_order.xml)
- Resource file prefixes indicate type (e.g., ic_/bg_)
- Package names use reverse domain notation (com.example.happucat)

Layered structure:
1. Base layer: libs/assets containing third-party dependencies
2. Resource layer: res/ for centralized UI resource management
3. Business layer: src/ organized by functional modules (not strictly MVVM)
4. Generated layer: gen/ automatically maintained by the system

Extension design:
1. Multi-resolution adaptation: drawable-*/values-* directory system
2. Modular design: Independent sharing module (cn.sharesdk)
3. Configuration separation: proguard-project.txt supports flexible obfuscation
4. Localization support: values/strings.xml as a multilingual extension point

Note: Potential optimization points:
- src/com/happycat directory could be further divided by functionality
- Business logic and UI not fully decoupled (e.g., Activity contains extensive business code)
- Missing clear network layer directory structure
```