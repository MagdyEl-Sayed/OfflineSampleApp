# Offline Sample App 

[![Build Status](https://travis-ci.org/jshvarts/OfflineSampleApp.svg?branch=master)](https://travis-ci.org/jshvarts/OfflineSampleApp)

## What is an Offline App?

Offline App (or Offline-First App) enables user to seamlessly interact with it by using local device storage and then synchronizing the data with some remote storage (cloud database, etc) later via a background process.

With offline apps
1) users no longer get error messages asking to try again later.
2) users do not see any loading bar since all actions are performed almost instantly using local storage.
3) users benefit from faster loading times and conserving battery life.

## Project Overview

This Android app is a working sample app that showcases offline photo commenting functionality. Users are able to comment on a photo using and comments are first stored in local Room database. This action kicks off a background job (implemented using Android Priority JobQueue library) to synchronize this data whenever the device is connected to the Internet. The job is persistent and is guaranteed to execute even if users restart their app or their device while waiting for network connection.        

## Libraries

* Patterns and frameworks
	* MVVM (Model-View-ViewModel) using Google's new Architecture components `ViewModel`, `LiveData`, etc.
	* [Clean Architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html) with `ViewModel` interacting with UseCases and the latter interacting with local database. Making each layer highly testable.
* Database
	* [Room Persistence Library](https://developer.android.com/topic/libraries/architecture/room.html), part of Google's new Architecture components.
* Background Job processing
	* [Android Priority JobQueue](https://github.com/yigit/android-priority-jobqueue) which uses [Job Scheduler](https://developer.android.com/reference/android/app/job/JobScheduler.html) for API level Lollipop and above and [GcmNetworkManager](https://developers.google.com/android/reference/com/google/android/gms/gcm/GcmNetworkManager) for API level below Lollipop.
* Remote Call APIs
	* [Retrofit 2](http://square.github.io/retrofit/) to perform HTTP requests.
	* Fake remote database using simple [JSONPlaceholder](https://jsonplaceholder.typicode.com) REST API.
* Dependency Injection
    * [Dagger Android 2.11](https://github.com/google/dagger/releases/tag/dagger-2.11) to manage App and Activity-scoped dependencies.
* Communication between app layers
    * [RxJava2](https://github.com/ReactiveX/RxJava) and [RxAndroid](https://github.com/ReactiveX/RxAndroid) for interacting between `ViewModel` and local database. 
    * [EventBus](http://greenrobot.org/eventbus/) for posting requests from the background job to lifecycle-aware Android components such as `Activity`. 
* Other
    * [ButterKnife](http://jakewharton.github.io/butterknife/) to simplify View and Listener bindings.

## License

    Copyright 2017 James Shvarts

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

