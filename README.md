# Personal Weather Station Plugin for FM-DX Webservers

This plugin allows real-time display of personal weather station data on [FM-DX webservers](https://github.com/NoobishSVK/fm-dx-webserver).
<br>
<br>
To do this, it communicates with the WeatherUnderground API and displays weather readings, updated at specific minute intervals.
<br>
<br>
⚠️ <b>Important note: This plugin is intended solely for owners of personal weather stations who contribute to WeatherUnderground by sending their station's data to the site, as contributing is a requirement for obtaining an API key.</b>
<br>
<b>If you do not have a personal weather station that sends data to WeatherUnderground, you will unfortunately not be able to use it.</b>
<br>
<br>
This plugin is a modified version of the ["Weather Plugin" made by NoobishSVK](https://github.com/NoobishSVK/fm-dx-webserver-plugin-weather), to make it compatible with personal stations.
<br>
<br>
<img width="566" height="517" alt="plugin-meteo-2" src="https://github.com/user-attachments/assets/9d39b4c6-faf3-4e86-bbd2-0f7ef8ae44d7" />

## Installation

1 - Download the entire repository as a ZIP file [by clicking here](https://github.com/LucasGallone/FMDX_PersonalWeatherStation/archive/refs/heads/main.zip).
<br>
<br>
2 - Extract the ZIP file content.
<br>
<br>
3 - Place the `PersonalWeatherStation.js` file and the `PersonalWeatherStation` folder in the plugins folder of your FM-DX webserver.
<br>
<br>
4 - Start/restart your FM-DX webserver.
<br>
<br>
5 - Access your webserver's configuration panel by using the admin account, click "Plugins" and select "Personal Weather Station by Lucas Gallone" in the plugins list, then save the changes.
<br>
<br>
6 - Restart your webserver. A message regarding the plugin should appear in the console. Once it is displayed, stop your server.
<br>
<br>
7 - Go to the `plugins_configs` folder of your webserver, and open the `PersonalWeatherStation.json` file with Notepad (Windows) / Nano (Linux). 
<br>
<br>
8 - Add the required information to this file regarding your weather station ID, API key, and station model (optional).
<br>
If you are unsure how to proceed, follow the instructions in the "Configuration" section below.
<br>
(You can also modify the other values, such as the units or the update interval, ​​if you wish.)
<br>
<br>
9 - Once the file is saved, restart your webserver. The plugin should appear, displaying your weather station's data.
<br>
If you obtain "No data available", verify your station's ID and API key, then try again.

## Configuration

Once the installation is complete, following the instructions above, you will need to configure your weather station so that the plugin can recognize it and retrieve its data.
- - -
The first step is to obtain your weather station's ID. To do this, log in to your WeatherUnderground account.
<br>
Once logged in, click on "My Profile" and then on "My Devices".
<br>
<br>
You should see your weather station appearing. Simply take note of your station's public ID (IBRIND40 in this case).
<br>
Ignore the "Key" value displayed on this page, it is not the one we need for the API.
<br>
<br>
<img width="1628" height="512" alt="wu-devices" src="https://github.com/user-attachments/assets/284b2b41-8de3-4c5f-a062-599c991b9c61" />
- - -
Once you have noted your ID, click on "API Keys", then the "Generate Key" button.
<br>
<br>
Your API key should appear instantly, as shown in the screenshot below. Click "Show Key" to reveal it.
<br>
Copy and paste it, or write it down.
<br>
<br>
(Note: The API key expires 6 months after the generation date. You will then need to generate a new one and update the JSON file to continue displaying your station's data.)
<br>
<br>
<img width="1151" height="628" alt="wu-api" src="https://github.com/user-attachments/assets/ae261b07-4a32-48e5-8f3a-0daf2b0be8d2" />
- - -
Open the `PersonalWeatherPlugin.json` file, located in the `plugins_configs` folder, with Notepad or Nano, and enter the previously noted station ID in quotation marks as the `stationId` value.
<br>
<br>
Then, specify the API key noted earlier, enclosed in quotation marks, as the `apiKey` value.
<br>
<br>
Although optional, it is recommended to specify the make and model of your weather station as the `stationModel` value. This allows visitors to your webserver to know what equipment you are using.
<br>
<br>
If you wish to use the metric system, leave the `unitSystem` value as is. Otherwise, change it to `imperial`.
<br>
<br>
By default, the plugin queries WeatherUnderground every 3 minutes to retrieve data from your station.
<br>
If you wish to change this interval, modify the `updateIntervalMinutes` value. The minimum value is 1.
<br>
<br>
Below all these values, you can choose to hide certain weather elements, such as wind speed and solar radiation. By default, all these elements are enabled.
<br>
If you wish to hide one, change the value of the element in question to `false`.

## Note on how API requests work

Regardless of the `updateIntervalMinutes` value used, requests to the WeatherUnderground API are sent only when at least one user is connected to your server.
<br>
If no one is connected, requests transmission is paused. The interval applies only when one or more users are present on the server.
<br>
<br>
A request is triggered immediately when the first user connects. If a second user visits your server while the first is still connected, they will see the weather station data without a new API request being made specifically for them.
<br>
<br>
Requests are sent by the host machine running your server, and not by your visitors, in order to protect your API key and limit the amount of requests not to exceed the daily quota.

## The plugin displays "No data available". What should I do?

• If you have just set up the plugin, you may have made a mistake when entering your station ID or API key.
<br>
-> Check both values ​​and try again.
<br>
<br>
• Your API key may have expired. Log in to your WeatherUnderground account, then click on "My Profile", "Member Settings", and "API Keys".
<br>
-> If you find that the key has expired, generate a new one and update the JSON configuration file.
<br>
<br>
• WeatherUnderground's servers may be temporarily inaccessible.
<br>
-> Please wait a moment and try again. You can try connecting to weatherunderground.com to verify if the website works.
<br>
<br>
• In rarer cases, the host machine may refuse to connect to the WeatherUnderground's servers.
<br>
-> Check your settings to ensure that no network restrictions are enabled.
