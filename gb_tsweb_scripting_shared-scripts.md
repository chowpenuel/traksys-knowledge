# Shared Scripts

Shared Scripts can be defined centrally under the Shared Scripts Hub of the Developer Section.

## Use

Shared Scripts can be used for creating classes or extensions which can be implemented and accessed throughout the entire TrakSYS development environment. This includes Logic (Service) Scripts (including Script Tags), Web Scripts (and the entire web development environment, such as Page Definition Scripts and Content Page Scripts), and Data Management Service Module Scripts.

## Best Practices

Shared Scripts must be Full Compiled using the button at the top of the HTML5 Script Editor. This will fully compile and publish the code for use within the TrakSYS development environment. Note that Service restarts may be necessary depending on where the script classes are implemented. For example, if a class defined in a Shared Script is used in a Script Tag, then the Logic Service must be restarted.
