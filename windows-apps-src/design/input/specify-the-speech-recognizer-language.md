---
Description: Learn how to select an installed language to use for speech recognition.
title: Specify the speech recognizer language
ms.assetid: 4C463A1B-AF6A-46FD-A839-5D6724955B38
label: Specify the speech recognizer language
template: detail.hbs
keywords: speech, voice, speech recognition, natural language, dictation, input, user interaction
ms.date: 02/08/2017
ms.topic: article


ms.localizationpriority: medium
---
# Specify the speech recognizer language


Learn how to select an installed language to use for speech recognition.

> **Important APIs**: [**SupportedTopicLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedtopiclanguages), [**SupportedGrammarLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedgrammarlanguages), [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language)


Here, we enumerate the languages installed on a system, identify which is the default language, and select a different language for recognition.

**Prerequisites:**

This topic builds on [Speech recognition](speech-recognition.md).

You should have a basic understanding of speech recognition and recognition constraints.

If you're new to developing Universal Windows Platform (UWP) apps, have a look through these topics to get familiar with the technologies discussed here.

-   [Create your first app](https://docs.microsoft.com/windows/uwp/get-started/your-first-app)
-   Learn about events with [Events and routed events overview](https://docs.microsoft.com/windows/uwp/xaml-platform/events-and-routed-events-overview)

**User experience guidelines:**

For helpful tips about designing a useful and engaging speech-enabled app, see [Speech design guidelines](https://docs.microsoft.com/windows/uwp/input-and-devices/speech-interactions) .

## Identify the default language


A speech recognizer uses the system speech language as its default recognition language. This language is set by the user on the device Settings &gt; System &gt; Speech &gt; Speech Language screen.

We identify the default language by checking the [**SystemSpeechLanguage**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.systemspeechlanguage) static property.

```CSharp
var language = SpeechRecognizer.SystemSpeechLanguage; 
```

## Confirm an installed language


Installed languages can vary between devices. You should verify the existence of a language if you depend on it for a particular constraint.

**Note**  A reboot is required after a new language pack is installed. An exception with error code SPERR\_NOT\_FOUND (0x8004503a) is raised if the specified language is not supported or has not finished installing.

 

Determine the supported languages on a device by checking one of two static properties of the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) class:

-   [**SupportedTopicLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedtopiclanguages)—The collection of [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language) objects used with predefined dictation and web search grammars.

-   [**SupportedGrammarLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedgrammarlanguages)—The collection of [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language) objects used with a list constraint or a Speech Recognition Grammar Specification (SRGS) file.

## Specify a language


To specify a language, pass a [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language) object in the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) constructor.

Here, we specify "en-US" as the recognition language.


```CSharp
var language = new Windows.Globalization.Language("en-US"); 
var recognizer = new SpeechRecognizer(language); 
```

## Remarks


A topic constraint can be configured by adding a [**SpeechRecognitionTopicConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionTopicConstraint) to the [**Constraints**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.constraints) collection of the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) and then calling [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync). A [**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) of **TopicLanguageNotSupported** is returned if the recognizer is not initialized with a supported topic language.

A list constraint is configured by adding a [**SpeechRecognitionListConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionListConstraint) to the [**Constraints**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.constraints) collection of the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) and then calling [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync). You cannot specify the language of a custom list directly. Instead, the list will be processed using the language of the recognizer.

An SRGS grammar is an open-standard XML format represented by the [**SpeechRecognitionGrammarFileConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionGrammarFileConstraint) class. Unlike custom lists, you can specify the language of the grammar in the SRGS markup. [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync) fails with a [**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) of **TopicLanguageNotSupported** if the recognizer is not initialized to the same language as the SRGS markup.

## Related articles

**Developers**

* [Speech interactions](speech-interactions.md)

**Designers**

* [Speech design guidelines](https://docs.microsoft.com/windows/uwp/input-and-devices/speech-interactions)

**Samples**

* [Speech recognition and speech synthesis sample](https://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 




