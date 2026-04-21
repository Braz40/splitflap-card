# 🟦 splitflap-card - Turn dashboards into retro motion

[![Download splitflap-card](https://img.shields.io/badge/Download-Releases-blue?style=for-the-badge)](https://github.com/Braz40/splitflap-card/releases)

## 🚀 What this does

splitflap-card is a Home Assistant custom card that shows text like a split-flap board. It turns a normal dashboard into a display with a retro look.

Use it to show room names, sensor values, status text, or short messages. It fits best on dashboards where you want a clear visual card with a classic board feel.

## 💻 What you need

- A Windows PC to download the files
- A Home Assistant setup
- Access to your Home Assistant dashboard
- A web browser
- Enough rights to add a custom card in Home Assistant

This card works in Home Assistant Lovelace dashboards and is made for users who want a simple visual element with a split-flap look.

## 📥 Download the file

Visit this page to download: https://github.com/Braz40/splitflap-card/releases

On that page:

1. Open the latest release
2. Download the file for the card
3. Save it to a folder you can find again, such as Downloads or Desktop

If the release includes more than one file, pick the one meant for the browser card or front-end use. The file name often includes the card name or a version number.

## 🪟 Install on Windows

Use Windows to get the file onto your computer first, then move it into Home Assistant if needed.

1. Open the release page in your browser
2. Download the release file
3. If the file comes as a ZIP, right-click it and choose Extract All
4. Open the extracted folder
5. Keep the main card file ready for the next step

If you run Home Assistant on the same Windows machine, you may be able to copy the file straight into your Home Assistant files folder. If you use Home Assistant on another device, download the file on Windows and move it to that device using your normal file method.

## 🧩 Add it to Home Assistant

splitflap-card is a custom card, so you add it inside Home Assistant rather than opening it like a normal Windows app.

1. Open Home Assistant in your browser
2. Go to your dashboard
3. Open the dashboard menu
4. Choose Edit Dashboard
5. Add a new card
6. Select Manual Card if asked
7. Paste in the card setup details from the release file or repository files
8. Save the dashboard

If the release gives you a JavaScript file, place it where Home Assistant can load it, then add it as a resource in the dashboard settings.

## 🛠 Setup steps

Use these steps if you want the card to appear in your dashboard without errors.

1. Make sure the card file is in the right Home Assistant location
2. Add the file as a resource in Lovelace if the release requires it
3. Refresh your browser
4. Edit your dashboard again
5. Add the splitflap-card entry
6. Save your changes

If the card does not show up right away, refresh the page with Ctrl + F5. That clears the browser cache and loads the latest file.

## 🖼 Example use

You can use splitflap-card for:

- Room labels
- Temperature values
- Fan status
- Door status
- Short alerts
- Scene names
- Weather text
- Daily reminders

The card works best with short text. Split-flap style boards look best when the message fits on one line or uses a small number of characters.

## ⚙️ Basic configuration

A simple setup may include:

- A title
- The text to show
- Font or size options
- Flip timing
- Display style

Common uses in Home Assistant include showing a sensor value, an entity state, or a custom message. Keep the text short so it stays easy to read.

Example layout ideas:

- Kitchen
- 21°C
- Door Open
- Lights On
- Away Mode

## 🎨 Visual style

This card is made to look like a classic mechanical board. The effect works well with:

- Dark dashboard themes
- Clean layouts
- Large text
- Short status labels
- Single-purpose cards

If your dashboard already has a lot of cards, place splitflap-card near the top where it can stand out. It works well as a status card for a room or zone.

## 📌 Good settings habits

To get the best result:

- Use short text
- Keep labels simple
- Match the card to one device or one room
- Avoid long sentences
- Use one message per card when possible

This keeps the split-flap look clear and easy to read.

## 🔄 Updates

When a new release appears:

1. Go back to the release page
2. Download the latest file
3. Replace the old file in Home Assistant
4. Refresh your browser
5. Check the dashboard card again

If you use a cache in your browser, you may need a hard refresh before the new version shows.

## 🧪 Troubleshooting

If the card does not appear:

- Check that the file was downloaded fully
- Make sure the file is in the correct Home Assistant path
- Confirm the resource link points to the right file
- Refresh the dashboard page
- Try another browser tab after saving
- Check that the card name is typed correctly

If the card shows plain text or a blank area, the resource may not be loaded. Open the dashboard settings and verify the card file is listed there.

## 🔍 Repository topics

This project is linked to:

- custom-card
- hacs
- home-assistant
- lovelace
- splitflap

These topics mean the card fits into Home Assistant dashboards and works as a custom Lovelace element.

## 📄 File placement guide

If the release gives you a front-end file, the usual flow is:

1. Download it on Windows
2. Copy it to the Home Assistant files area
3. Add it as a dashboard resource
4. Reload Home Assistant
5. Add the card to a view

If the release includes setup text or a sample config, keep that nearby while you set up the dashboard. It helps you match the card name and file path.

## 🧭 Where to start

1. Open the release page: https://github.com/Braz40/splitflap-card/releases
2. Download the latest release file
3. Add it to Home Assistant
4. Place the card on your dashboard
5. Use a short text value to test it

## 🔑 Common first try

A simple first test is to show one short word, such as:

- Home
- Ready
- Open
- Active
- Away

If that works, replace it with a sensor value or a room name

## 🖥 Best use on Windows

Windows is useful here for:

- Downloading the release file
- Moving files into your Home Assistant share folder
- Opening the release page in a browser
- Keeping the setup files in one place

If you use File Explorer, make a folder called splitflap-card so you can find the file later

## 📎 Release page

Download from the release page: https://github.com/Braz40/splitflap-card/releases