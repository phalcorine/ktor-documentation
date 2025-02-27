[//]: # (title: Adding client dependencies)

<show-structure for="chapter" depth="2"/>

<link-summary>Learn how to add client dependencies to the existing project.</link-summary>

To use the Ktor HTTP client in your project, you need to [configure repositories](#repositories) and add the following dependencies:
- **[ktor-client-core](#client-dependency)**

  `ktor-client-core` contains core Ktor client functionality. 
- **[Engine dependency](#engine-dependency)**

  Engines are used to process network requests. 
  Note that a [specific platform](client-supported-platforms.md) may require a specific engine that processes network requests.
- (Optional) **[Plugin dependency](#plugin-dependency)**

  Plugins are used to extend the client with a specific functionality.



<include from="server-dependencies.topic" element-id="repositories"/>


## Add dependencies {id="add-ktor-dependencies"}

> For [different platforms](client-supported-platforms.md), Ktor provides platform-specific artifacts with suffixes such as `-jvm` or `-js`, for example, `ktor-client-core-jvm`. Note that Gradle resolves artifacts appropriate for a given platform automatically, while Maven doesn't support this capability. This means that for Maven, you need to add a platform-specific suffix manually.
>
{type="tip"}

### Client dependency {id="client-dependency"}
The main client functionality is available in the `ktor-client-core` artifact. Depending on your build system, you can add it in the following way:

<var name="artifact_name" value="ktor-client-core"/>
<include from="lib.topic" element-id="add_ktor_artifact"/>

You can replace `$ktor_version` with the required Ktor version, for example, `%ktor_version%`.

For a multiplatform project, you need to add the `ktor-client-core` artifact to the `commonMain` source set:

```kotlin
```
{src="snippets/tutorial-client-kmm/shared/build.gradle.kts" include-lines="19-23,25-26,59"}




### Engine dependency {id="engine-dependency"}
An [engine](http-client_engines.md) is responsible for processing network requests. There are different client engines available for various platforms, such as Apache, CIO, Android, iOS, and so on. For example, you can add a `CIO` engine dependency as follows:

<var name="artifact_name" value="ktor-client-cio"/>
<include from="lib.topic" element-id="add_ktor_artifact"/>

For a multiplatform project, you need to add a dependency for the required engine to a corresponding source set.
For example, the code snippet below shows how to add the `ktor-client-okhttp` dependency to the `androidMain` source set:

```kotlin
```
{src="snippets/tutorial-client-kmm/shared/build.gradle.kts" include-lines="19-20,32-36,59"}

For a full list of dependencies required for a specific engine, see [](http-client_engines.md#dependencies).


### Plugin dependency {id="plugin-dependency"}
Ktor lets you use additional client functionality ([plugins](http-client_plugins.md)) that is not available by default, for example, logging, authorization, or serialization. Some of them are provided in separate artifacts. You can learn which dependencies you need from a topic for a required plugin.

> For a multiplatform project, a plugin dependency should be added to the `commonMain` source set. Note that some plugins might have  [limitations](http-client_engines.md#limitations) for specific platforms.
