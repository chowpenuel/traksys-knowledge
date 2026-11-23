# Service and Model Philosophy

The TrakSYS API consists of two types of objects : Services and Models.

## Models

Models are data objects that represent a certain type of data entity in the TrakSYS database (an Event for example). Models are structures only, with no corresponding code (Methods or Events) exposed from the object. All of the Model classes are defined in the ETS.Core.Api.Models namespace.

## Services

Services are objects that act on and return Model objects. The Service classes and their methods are stateless. All state in an application of the API is maintained using Model classes that are passed in and out of the API using the Services. The Service classes can be accessed with an instance of the `ETS.Core.Api.ApiService object`.
