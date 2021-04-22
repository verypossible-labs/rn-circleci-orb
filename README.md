# React Native CircleCI Orb

A [CircleCI Orb](https://circleci.com/orbs/) for building and deploying React Native apps.

This orb is a fork of [React Native Community's CirleCI Orb](https://github.com/react-native-community/react-native-circleci-orb.git) with a few changes.

There are several nuances when it comes to CI/CD with React Native: which machines to use, caching, etc. This orb simplifies the process in addition to making the build process for mobile projects at [Very](https://verypossible.com) consistent.

## Getting Started

We recommend reading the [Using Orbs](https://circleci.com/docs/2.0/using-orbs/) guide from the CircleCI documentation to get an overview of how to use Orbs.

This Orb provides three different categories of tools to help you build and test your React Native app on CircleCI:

- **Executors**: Machines which are configured for use with React Native.
- **Commands**: Individual tasks which you can piece together in your own jobs to perform tasks like installing dependencies, building an APK, or running Detox tests.
- **Jobs**: Groups of commands which are typically used together as a stage in a pipeline.

### Setup

**⚠️ Important:** You will need a macOS plan enabled for building iOS apps and for e2e testing on iOS and Android. Private projects require a payment plan for this.

1. Inside CirleCI, enable these settings:

- **3rd party orbs**: `Your Org -> Settings -> Security -> Enable Usage of 3rd Party Orbs`
- **Pipelines**: `Project Settings -> Advanced Settings -> Pipelines`

2. Use CircleCI version 2.1 at the top of your `.circleci/config.yml`

```yml
version: 2.1
```

3. Invoke the orb in your config:

```yml
orbs:
  rn: verypossible/react-native@1.0.0
```

You can now use elements from the orb in your workspace by prefixing them with `rn`. You can change `rn` to anything you'd like.

4. **Android only**: Add this task in `android/app/build.gradle`

```java
task downloadDependencies() {
  description 'Download all dependencies to the Gradle cache'
  doLast {
    configurations.findAll().each { config ->
      if (config.name.contains("minReactNative") && config.canBeResolved) {
        print config.name
        print '\n'
        config.files
      }
    }
  }
}
```

## Usage

See the [examples](./src/examples).

## Roadmap

Please see the [open issues](https://github.com/verypossible-labs/rn-circleci-orb/issues) for a list of known issues / proposed features.

## Contributing

Contributions are welcome! Any contributions you make are greatly appreciated. Please see [CONTRIBUTING.md](./CONTRIBUTING.md) and our [Code of Conduct](./CODE_OF_CONDUCT.md).

## License

Distributed under the [MIT license](https://github.com/verypossible-labs/rn-circleci-orb/blob/master/LICENSE)

## Acknowledgements

- [@react-native-community/circleci-orb](https://github.com/react-native-community/react-native-circleci-orb.git)
