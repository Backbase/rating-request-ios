# Request App Store rating (iOS)
This repository contains implementation of requesting an App Store rating functionality for a Backbase iOS application

## Description
"Rating Request" implementation lets you request App Store rating from the users of a Backbase application. The implementation is flexible enough to be used in any place of the application as required and configurable on the frequency (at the moment it's number of months).

![AppStoreRatingExample](./Documents/rating_request_example.gif)

## Table of Contents

- [Requirements](#requirements)
- [Environment Setup](#environment-setup)
- [Official Guidelines](#official-guidelines)

---
### Requirements
Mobile SDK 10.1.0 or higher is recommended due to Backbase Secure Storage usage.

---
### Environment Setup

> Follow steps in this section if you are setting up the project for the first time, otherwise, skip to the next [section](#project-generation).

Before building the project make sure all above requirements are installed on your device.

#### 1. Install [Homebrew](https://brew.sh/)

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### 2. Install [Bundler](https://bundler.io/)

```sh
gem install bundler
```

#### 3. Set artifactory credentials

repo-art uses authentication as specified in your standard [netrc](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html) file.

Log in to Artifacts and click on your name in the top right. Enter your password again and click "Unlock". Next to the "Encrypted Password" field, copy your encrypted password by clicking the "Copy encrypted password to clipboard" button.

Open **~/.netrc** on your computer. If this file does not exist, create it.
Add the following 3 lines to the file, replacing `{username}` with your artifactory username and `{encrypted password}` with the encrypted password you just copied.

```txt
machine repo.backbase.com
  login {username}
  password {encrypted password}
```

#### 4. Install build dependencies

> Within the project directory:

```sh
bundle install
```

#### 5. Add required artifactory repositories

```sh
bundle exec pod repo-art add bbartifacts3 https://repo.backbase.com/api/pods/ios3
bundle exec pod repo-art add bbartifacts-retail3 https://repo.backbase.com/api/pods/ios-retail3

```

#### 6. Update artifactory repositories

```sh
bundle exec pod repo-art update bbartifacts3
bundle exec pod repo-art update bbartifacts-retail3
```

> Having a hard time with Ruby? see [troubleshooting](#troubleshooting).

---

### Official Guidelines
Please review official [Apple Guidelines](https://developer.apple.com/documentation/storekit/requesting-app-store-reviews) for requesting App Store Ratings from users.

## Test App
"RatingRequestApp" is a test app that includes one ViewController which has the code to trigger an App Store rating in ```viewDidAppear(_ animated:)``` method as an example.

---
## Invoke App Store review
```swift
        // Request app store review, with 3 months frequency.
        // this will not request another review request for 3 months

        let ratingRequestManager = RatingRequestManager(configuration: .init(frequencyInMonths: 3))
        ratingRequestManager.requestReviewIfAppropriate()
```

---
## LTS version supported
This implementation is supported from 2023.09 LTS onwards.

---
## Troubleshooting

### Ruby related problems

Install [rbenv](https://github.com/rbenv/rbenv)

> rbenv is a tool that lets you install and run multiple versions of Ruby side-by-side. It's simple, lightweight, and reliable.

```sh
brew update && brew install rbenv ruby-build
```

Add the following lines to your profile file

> Your profile file is **~/.zshrc** if you are using Z shell, or **~/.bash_profile** if you are using Bash

```bash
export PATH="/usr/local/opt/ruby/bin:$PATH"
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```

> In your project directory, install ruby version required for the project

```sh
rbenv install
```

Then continue the flow in the as in the **Getting Started** section.

### Test the App Store rating requests in accordance to the [official guidelines](#official-guidelines)

---
## License

Backbase License. See [LICENSE](LICENSE) for more info.
