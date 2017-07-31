##########
Voicemail
##########


To edit voicemail settings click the pencil edit icon on the right of the extension number.

.. image:: ../_static/images/fusionpbx_voicemail.jpg
        :scale: 85%


Here you can edit voicemail settings.

*  Greeting- When you dial *97, record a greeting and set a number you can choose which greeting to use
*  Options- Can create a voicemail IVR
*  Mail to- have voicemails emailed to this address
*  Voicemail File- Auto File Attachment, Listen Link, Download Link
*  Keep Local- To keep the voicemail on the server after being emailed or not
*  Forward Destinations- Forward voicemail messages to additional destinations
*  Enabled- Enable or disable the voicemail box

.. image:: ../_static/images/fusionpbx_voicemail1.jpg
        :scale: 85%


Voicemail Options
====================


Access an extensions voicemail **away** from the extension dial the extension and interupt the greeting with the ***star** key.

+-------------+-----------------------+------------------------------+-----------------------------------+
| ***97**     | To access **that** extensions voicemail **from the extension** or the voicemail button   |
+-------------+-----------------------+------------------------------+-----------------------------------+
| ***98**     | To access **any** extensions voicemail                                                   |
+-------------+-----------------------+------------------------------+-----------------------------------+
| ***99[ext]**| To access **a specific** extension voicemail                                             |
+-------------+-----------------------+------------------------------+-----------------------------------+


+-------------+-----------------------+
|             |   **Main Menu**       |
+-------------+-----------------------+
| **press 5** | For advanced options  |
+-------------+-----------------------+


+-------------+-----------------------+
|             | **Advanced Options**  |
+-------------+-----------------------+
| **press 1** | Record a greeting     |
+-------------+-----------------------+
| **press 2** | Choose a greeting     |
+-------------+-----------------------+
| **press 3** | Record name           |
+-------------+-----------------------+
| **press 6** | Change password       |
+-------------+-----------------------+
| **press 0** | For main menu         |
+-------------+-----------------------+


*****************
Voicemail Transcription
*****************

|

Uses API services to transcribe voicemails into text to be used in the app-sms and the voicemail to email options. Currently (11/3/16) only supports microsoft bing

Sign up and language information is located on `Microsoft Site <https://www.microsoft.com/cognitive-services/en-us/Speech-api/documentation/API-Reference-REST/BingVoiceRecognition>`_

.. warning:: We cannot use mod_shout to record Voicemails because the transcription service needs an uncompressed version of the audio. Therefore we will record in WAV and then use LAME to re-encode in MP3. This could cause added resource utilization to your system.

**Goto Advanced > Default Settings.**
Add the following entries

+-------------+-----------------------+-----------+---------------------------+-----------+
|  Category   |  Subcategory          |  Type     |  Value                    |  Enabled  |
+=============+=======================+===========+===========================+===========+
|  voicemail  |  transcribe_provider  |  text     |  microsoft                |  True     |
+-------------+-----------------------+-----------+---------------------------+-----------+
|  voicemail  |  microsoft_key1       |  text     |  {your microsoft key #1}  |  True     |
+-------------+-----------------------+-----------+---------------------------+-----------+
|  voicemail  |  microsoft_key2       |  text     |  {your microsoft key #2}  |  True     |
+-------------+-----------------------+-----------+---------------------------+-----------+
|  voicemail  |  transcribe_language  |  text     |  en-US                    |  True     |
+-------------+-----------------------+-----------+---------------------------+-----------+
|  voicemail  |  transcribe_enabled   |  boolean  |  true                     |  True     |
+-------------+-----------------------+-----------+---------------------------+-----------+
 
 Click "Reload" at the top of the page.
 
**Goto Status > Sip Status.**

Click "Flush Memcache", "Reload XML" and "Rescan".
 
If you entered your key's correctly, you should now start getting transcriptions delivered in your voicemail to email and you will also see them on the Messages page.
