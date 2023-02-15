# WizardWorld

Clean Architecture app using the 
[WizardWorld API](https://wizard-world-api.herokuapp.com/swagger/index.html) and following 
'Modern Android Development Skills' recommendations with Android Jetpack libraries.

## Clean Architecture

This app is engineered following Clean Architecture principles;
To achieve that we have the following modules:
- `app`: Android application module providing interface implementations to the layer modules.
- `ui`: Android library made of UI components + ViewModels (MVVM)
- `domain`: pure Kotlin library implementing domain logic and orchestrating Repositories to perform 
actions and manage states.
- `data`: pure Kotlin library having Repository implementations and data mapping for the domain 
layer.
- `datasource`: Android library having DataSource implementations to local and remote resources.

The `domain` and `data` modules are pure Kotlin libraries, without knowledge of the Android 
framework, following the Clean Architecture principle saying that the framework and the platform 
should be a detail, leaving operational code unaware of those and independent, clean.

The `datasource` module is dependent on the platform to implement real datasource instances as they 
have to be bound to an Android Context, and the module uses `data` models to serialize both local 
and remote resources.

```           
           ┌────┐
        ┌──► ui │
        │  └───┬┘
        │      │
        │      │
        │  ┌───▼────┐
        ├──► domain │
        │  └───▲────┘
┌─────┐ │      │
│ app ├─┤      │
└─────┘ │      │
        │  ┌───┴──┐
        ├──► data │
        │  └───▲──┘
        │      │
        │      │
        │  ┌───┴────────┐
        └──► datasource │
           └────────────┘
```