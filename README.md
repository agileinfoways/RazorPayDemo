# Documentation

Following items are considered while integrating RazorPay in your application:

- Follow proper installation process from official site. [(refer link number 1 or 2 for more details)](#some-useful-links)
- Version used for RazorPay integration, but one must use latest version
    >"react-native-razorpay": "^2.0.20"
- Must use _Xcode 11.1_ or above version for RazorPay Integration
- Must add script in Build Phase. [(refer link number 4 for more details)](#some-useful-links)

```markdown
    APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"

    # This script loops through the frameworks embedded in the application and
    # removes unused architectures.
    find "$APP_PATH" -name '*.framework' -type d | while read -r FRAMEWORK
    do
        FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)
        FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"
        echo "Executable is $FRAMEWORK_EXECUTABLE_PATH"

        EXTRACTED_ARCHS=()

        for ARCH in $ARCHS
        do
            echo "Extracting $ARCH from $FRAMEWORK_EXECUTABLE_NAME"
            lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"
            EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")
        done

        echo "Merging extracted architectures: ${ARCHS}"
        lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"
        rm "${EXTRACTED_ARCHS[@]}"

        echo "Replacing original executable with thinned version"
        rm "$FRAMEWORK_EXECUTABLE_PATH"
        mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"

    done
    ```
- Verify that you enabled necessary things in build setting. [(refer link number 3 or 5 for more details)](#some-useful-links)

## Some Useful Links

- For RazorPay manual installation process (Github)
  <https://github.com/razorpay/react-native-razorpay/wiki/Manual-Installation-Steps>
- For RazorPay installation process (Official Doc)
  <https://razorpay.com/docs/payment-gateway/react-native-integration/custom/>
- Used for fixing iOS issue 
  <https://github.com/razorpay/react-native-razorpay/issues/174>
- For adding Run Script in Build Phases
  <https://stackoverflow.com/questions/30547283/submit-to-app-store-issues-unsupported-architecture-x86>
- <https://user-images.githubusercontent.com/6712500/56489109-3ed30b80-64fe-11e9-933f-66052b994c0f.png>