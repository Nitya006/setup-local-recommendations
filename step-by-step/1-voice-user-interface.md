# Build An Alexa Local Recommendations Skill
[Voice User Interface](/step-by-step/1-voice-user-interface.md) || [Lambda Function](/step-by-step/2-lambda-function.md) || [Connect VUI to Code](/step-by-step/3-connect-vui-to-code.md) || [Testing](/step-by-step/4-testing.md) || [Customization](/step-by-step/5-customization.md) || [Intents and Slots](/step-by-step/6-intents-slots.md) || [Smart Recommendations](/step-by-step/7-smart-recommendations.md) || [Alexa Design](/step-by-step/8-alexa-design.md) || [IoT](https://github.com/voicehacks/alexa-iot/blob/master/README.md) || [Publication](/step-by-step/10-publication.md)



## Setting up Your Voice User Interface

There are two parts to an Alexa skill.  The first part is the [Voice User Interface (VUI)](https://developer.amazon.com/alexa-skills-kit/vui).  This is where we define how we will handle a user's voice input, and which code should be executed when specific commands are uttered.  The second part is the actual code logic for our skill, and we will handle that in [the next step](../step-by-step/2-lambda-function.md) of this step-by-step guide.

1.  **Go to the [Amazon Developer Portal](http://developer.amazon.com).  In the top right corner of the screen, click the Sign In button.** </br>(If you don't already have an account, you will be able to create a new one for free.)

    ![Sign in](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/1-1-developer-portal._TTH_.png)

2.  **Once you have signed in, click the Alexa button at the top of the screen.**

    ![Alexa button](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/1-2-alexa-button._TTH_.png)

3.  **On the Alexa page, choose the Get Started button for the Alexa Skills Kit.**

    ![Get Started](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/1-3-alexa-skills-kit._TTH_.png)

4.  **Select Add A New Skill.** This will get you to the first page of your new Alexa skill.

    ![Amazon Developer Portal](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/1-4-add-a-new-skill._TTH_.png)

5.  **Fill out the Skill Information screen.**  Make sure to review the tips we provide below the screenshot.

    ![Skill Information](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/1-5-skill-information._TTH_.png)

    ### Skill Information Instructions
    *  **Skill Type** For this skill, we are creating a skill using the Custom Interaction Model.  This is the default choice.

    *  **Language** Choose the first language you want to support.  You can add additional languages in the future, but we need to start with one.  (This guide is using U.S. English to start.)

    *  **Name** This is the name of the skill as it will be displayed in the [Alexa app](http://alexa.amazon.com).

    *  **Invocation Name** This is the name spoken by your users to start the skill. Use a name like "local recommendations" for this sample skill. Some common issues that developers experience with invocation names are listed in the following table. In addition, please review the [Invocation Name Requirements](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/choosing-the-invocation-name-for-an-alexa-skill) as you consider an invocation name for your skill.

        | Invocation Name Requirements | Examples of incorrect invocation names |
        | ---------------------------- | -------------------------------------- |
        | The skill invocation name must not infringe upon the intellectual property rights of an entity or person. | korean air; septa check |
        | Invocation names should be more than one word (unless it is a brand or intellectual property), and must not be a name or place | horoscope; trivia; guide; new york |
        | Two word invocation names are not allowed when one of the words is a definite article, indefinite article, or a preposition | any poet; the bookie; the fool |
        | The invocation name must not contain any of the Alexa skill launch phrases and connecting words.  Launch phrase examples include "launch," "ask," "tell," "load," and "begin."  Connecting word examples include "to," "from," "by," "if," "and," "whether." | trivia game for star wars; better with bacon |
        | The invocation name must not contain the wake words "Alexa," "Amazon," "Echo," "Computer," or the words "skill" or "app." | hackster initial skill; word skills |
        | The invocation name must be written in each language you choose to support.  For example, the German version of your skill must have an invocation name written in German, while the English (US) version must have an invocation name written in English. | kitchen stories (German skill) |

    *  **Audio Player** For this Local Recommendations skill, we won't be using any audio files, so you can select No for this option.  If you would like to learn more about adding audio to your skills, please check out our [Audio Player Guide](https://github.com/alexa/skill-sample-nodejs-audio-player).

6.  **Click the Next button to move to the Interaction Model.**

    ![Next Button](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/1-6-next-button._TTH_.png)

7.  **Fill out the Interaction Model screen.**  Below the screenshot, we have provided links to the content you need to include in each box.

    ![Interaction Model](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/1-7-interaction-model._TTH_.png)

    ### Interaction Model Instructions
    1.  **Intent Schema** An intent schema defines the actions that we want our users to be able to take.  We will dive into modifying this schema later in this guide, so for now, just copy and paste this code into the Intent Schema box.
        ```javascript
                {
          "intents": [
            {
              "intent": "AboutIntent",  "slots":[]
            },

            {
              "intent": "CoffeeIntent",  "slots":[]
            },
            {
              "intent": "BreakfastIntent",  "slots":[]
            },
            {
              "intent": "LunchIntent",  "slots":[]
            },
            {
              "intent": "DinnerIntent",  "slots":[]
            },
            {
              "intent": "AttractionIntent",
              "slots":[
                { "name":"distance", "type":"AMAZON.NUMBER" }
              ]
            },
            {
              "intent": "GoOutIntent",  "slots":[]
            },
            {
              "intent": "AMAZON.YesIntent"
            },
            {
              "intent": "AMAZON.NoIntent"
            },
            {
              "intent": "AMAZON.HelpIntent"
            },
            {
              "intent": "AMAZON.StopIntent"
            },
            {
              "intent": "AMAZON.CancelIntent"
            }
          ]
        }
        ```
       ([get this on GitHub](../speech-assets/intent-schema.json))

        Note the AttractionIntent, which has a slot defined: distance.  Amazon provides Built-In Slots to handle commonly recurring sets. We've used these [Built-In Slots]((https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference#list-types)) to set the type for this slot: AMAZON.NUMBER.  Later in this course we will define a custom slot type. Let's continue ahead with what we have for now.


    2.  **Sample Utterances** Sample utterances guide Alexa to map what a user says to the Intents that we defined earlier. Copy these sample utterances and paste them into the **Sample Utterances** box in your browser.

        ```
        AboutIntent about
        AboutIntent tell me about this place

        CoffeeIntent coffee
        CoffeeIntent coffee shop

        BreakfastIntent breakfast
        LunchIntent lunch
        DinnerIntent dinner

        AttractionIntent recommend an attraction
        AttractionIntent recommend an attraction within {distance} miles

        AttractionIntent give me an activity
        AttractionIntent give me an activity within {distance} miles

        GoOutIntent go out
        GoOutIntent go outside
        GoOutIntent lets go out
        ```
        ([get this on GitHub](../speech-assets/sample-utterances.txt))

        When you have added these sample utterances to your skill, click **Save** to verify that your interaction model builds properly without any errors.

8.  If your interaction model builds successfully, click **Next** to move on to Configuration.  In our next step of this guide, we will be creating our Lambda function in the AWS developer console, but keep this browser tab open, because we will be returning here on [Page #3: Connect VUI to Code](../step-by-step/3-connect-vui-to-code.md).

    If you get an error from your interaction model, check through this list:

    *  **Did you copy and paste the provided code into the appropriate boxes?**
    *  **Did you accidentally add any unwanted characters to the Interaction Model or Sample Utterances?**

<br/><br/>
[![Next: Lambda Function](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/buttons/button_next_lambda_function._TTH_.png)](../step-by-step/2-lambda-function.md)

<img height="1" width="1" src="https://www.facebook.com/tr?id=1847448698846169&ev=PageView&noscript=1"/>
