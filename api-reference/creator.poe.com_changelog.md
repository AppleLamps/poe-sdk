---
url: "https://creator.poe.com/changelog"
title: "Changelog | Poe Creator Platform"
---

### Search

### Type

Bug FixNew FeatureImprovement

### Breaking

Breaking OnlyNon-Breaking Only

### Tags

Canvas AppsServer Bots

Improvementv1.0.5December 12, 2025

### App Creator and Script Bot Creator now use Claude-Opus-4.5 by default

App Creator and Script Bot Creator are now powered by Claude-Opus-4.5 by default, upgrading from Claude-Sonnet-4.5.

- Claude-Opus-4.5 completes tasks faster and with higher quality. Try the new experience at https://poe.com/App-Creator and https://poe.com/Script-Bot-Creator.

app-creatorscript-bot-creatorcanvas-appsclaude-agent-sdk

Improvementv1.0.4December 10, 2025

### Script Bot Creator now has default images for testing

Script Bot Creator now provides default test images that can be automatically used when testing your creations.

- Try the new experience at https://poe.com/Script-Bot-Creator.

claude-agent-sdkscript-bot-creator

Improvementv1.0.3December 2, 2025

### App Creator now supports changing the base model

You can now change the base model to Claude-Opus-4.5, Claude-Sonnet-4.5 or Claude-Haiku-4.5 via parameter controls.

- Try the new experience at https://poe.com/App-Creator.

app-creatorclaude-agent-sdkcanvas-apps

New Featurev1.0.2November 25, 2025

### Support for Multi User Chats

Replace enable\_multi\_bot\_chat\_prompting setting with enable\_multi\_entity\_prompting setting.

- Added enable\_multi\_entity\_prompting setting (defaults to True). When enabled, Poe modifies the previous chat history with special prompting

multi-botgroup-chatmulti-entity

Improvementv1.0.1November 11, 2025

### App Creator now generates improved, polished UI

App Creator now produces apps with improved design, styling, and layout by default, resulting in a more polished user experience.

- Try the new experience at https://poe.com/App-Creator.

app-creatorcanvas-apps

Improvementv1.0.0October 18, 2025

### App Creator can now access real-time information from the Web

- App Creator can now search the web to find the latest libraries, verify current documentation, research solutions, and more while building Canvas Apps
- Try it at https://poe.com/App-Creator

canvas-appsapp-creator

Improvementv1.0.0October 16, 2025

### App Creator is now powered by Claude Agent

The new App Creator is built on Claude Agent, the same system behind Claude Code, for more powerful code generation and editing.

- Try the new experience at https://poe.com/App-Creator
- You can still access the previous version at https://poe.com/App-Creator-1-Legacy

canvas-appsclaude-agent-sdkapp-creator

New Featurev1August 20, 2025

### Poe Usage API

Poe now supports two new endpoints for monitoring your recent usage and determining your current balance.

- /usage/current\_balance will tell you your current point balance.
- /usage/points\_history will return a paginated list of recent point usages, up to 30 days ago.

apienhancements

Improvementv0.0.68August 14, 2025

### Enhanced server bot tool calling

Server bots can now manage tool call loops and preserve tool call details in the chat for future user queries.

- Call stream\_request() with the tools field set (and leave tool\_executables as None) to get tool calls from the LLM.

server-botstools

New Featurev1.0.1August 9, 2025

### API Enhancements for Public Bots

Reliability and accessibility improvements for the API platform

- Fixed critical issue with prompt bots where prompts were not being properly transmitted through the API
- Added Assistant bot functionality to the public API, enabling new integration possibilities
- Resolved timeout issues during streaming operations, improving overall stability

apipublic-botsbug-fixesenhancements

New Featurev1.0.0August 1, 2025

### Poe API is now available for all public bots

Poe API is now available for all public bots. This allows you to use Poe API with your own interface or via the OpenAI compatible API.

- Use your existing Poe subscription points with no additional setup
- Access models across all modalities: text, image, video, and audio generation
- OpenAI-compatible interface works with existing tools like Cursor, Cline, Continue, and more
- Single API key for hundreds of models instead of managing multiple provider keys

apipublic-bots

New Featurev0.0.65July 1, 2025

### Parameter Controls

Feature release for Parameter Controls, a new setting that allows server bots to add additional input elements to their UI on Poe.

- Added Parameter Controls setting for server bots
- Allows server bots to add additional input elements to their UI
- Enables more interactive bot experiences

server-botsuiparameter-controls

Improvementv0.0.64July 1, 2025

### Add Headers to stream\_request()

client: add extra\_headers to stream\_request()

- Added extra\_headers parameter to stream\_request() function
- Enables custom headers in streaming requests

clientstream-requestheaders

Improvementv1.0.0June 19, 2025

### App Creator now uses Lyria by default for music generation

App Creator now uses Lyria by default to create apps with music generation features.

- Lyria is now the default music generation model in App Creator
- Enables creation of apps with music generation features
- Example: Make an app that allows users to upload images and generate music clips based on the image content

canvas-appslyriamusic-generation

New Featurev0.0.63June 15, 2025

### Add upload\_file and Enable File Input for Bot Query

Add a file upload function to client. This should enable file input for bot query requests.

- Added upload\_file function to client
- Enabled file input for bot query requests
- Improved file handling capabilities

file-uploadclientbot-query

Improvementv1.0.0June 3, 2025

### App Creator now uses Runway-Gen-4-Turbo by default for video generation

App Creator now uses Runway-Gen-4-Turbo by default to create apps with video generation features.

- Runway-Gen-4-Turbo is now the default video generation model
- Enables creation of apps with cinematic video generation
- Example: Make an app that brings photos to life with cinematic camera movements and atmospheric effects

canvas-appsrunwayvideo-generation

Improvementv1.0.0May 30, 2025

### App Creator improvements with Claude Sonnet 4

App Creator now always edits the latest version of your app code and is powered by Claude Sonnet 4.

- App Creator now always edits the latest version of your app code
- No longer supports editing older versions to avoid code edit failures
- Powered by Claude Sonnet 4 for improved performance
- Edits rather than rewrites code more frequently
- Makes less unsolicited edits
- Creates apps with improved UI

canvas-appsclaude-sonnet-4code-editing

Improvementv0.0.62May 15, 2025

### Increased server bot response limit

Previously the total length of a bot's response could not exceed 100,000 characters. This has now been updated to 512,000 characters. To see other limits visit https://creator.poe.com/docs/poe-protocol-specification#limits.

- Increased response limit from 100,000 to 512,000 characters
- Applies to all server bot responses
- Updated protocol specification with new limits

server-botslimitsresponse-length

Improvementv0.0.61May 15, 2025

### Bump protocol version to 1.1 and update SettingsResponse

The default values on SettingsResponse are changing in the next version of the Poe Protocol, and this updates fastapi\_poe to use the new version's functionality.

- Updated protocol version to 1.1
- Changed default values on SettingsResponse
- Updated fastapi\_poe to use new protocol functionality

protocolsettings-responsefastapi-poe

Improvementv1.0.0May 13, 2025

### App Creator HTML and JavaScript syntax checking

App Creator now automatically performs HTML and JavaScript syntax checking when editing code.

- Automatic HTML syntax checking during code editing
- Automatic JavaScript syntax checking during code editing
- Prevents syntax errors in generated apps

canvas-appssyntax-checkinghtmljavascript

Improvementv1.0.0May 12, 2025

### Improved parallel messaging handling

App Creator now handles combining /repeat and multiple at-mentions in parallel messaging more effectively.

- Better handling of /repeat command with multiple at-mentions
- Improved parallel messaging performance
- More effective combination of multiple commands

canvas-appsparallel-messagingrepeat-command

Improvementv1.0.0April 23, 2025

### App Creator now uses GPT-Image-1 by default for image generation

App Creator now uses GPT-Image-1 by default to create apps with image generation features.

- GPT-Image-1 is now the default image generation model
- Enables creation of apps with advanced image generation
- Example: Make an app that turns photos into 3D chibi anime style images

canvas-appsgpt-image-1image-generation

New Featurev1.0.0April 22, 2025

### Added support for file downloads and external links

Canvas apps now support file downloads and external links functionality.

- Added support for file downloads in canvas apps
- Added support for external links in canvas apps
- Example app: Drawing canvas with download button
- Example app: Website with links to other famous websites

canvas-appsfile-downloadsexternal-links

New Featurev1.0.0April 21, 2025

### Launched Remix for canvas apps

You can now remix eligible canvas apps using App Creator to customize them into your own unique versions.

- Remix feature launched for canvas apps
- Users can customize existing apps into unique versions
- Apps with remix enabled show a 'Remix' button in the header
- Creators can control whether their apps can be remixed
- Apps created before April 21, 2025 have Remix enabled by default

canvas-appsremixcustomization

New Featurev0.0.60April 15, 2025

### Server bot creators can define and explain variable pricing for their bots

New methods and settings for server bot creators to define and explain variable pricing for their bots.

- New method authorize\_cost: used to ensure the user is willing to spend enough points before you make potentially expensive model calls
- New method capture\_cost: used to capture the actual cost after you perform the model calls
- New setting cost\_label: used to show a short pricing string in the Poe UI (e.g. "100+ points")
- New setting rate\_card (previously custom\_rate\_card): used to provide a more detailed explanation of your pricing structure

server-botspricingcost-management

New Featurev0.0.59April 15, 2025

### Add get\_bot\_response\_sync

Add get\_bot\_response\_sync, which is a synchronous wrapper around get\_bot\_response. This allows users to call the function more easily without having to worry about asyncio.

- Added get\_bot\_response\_sync function
- Synchronous wrapper around get\_bot\_response
- Simplifies usage without requiring asyncio knowledge

syncwrapperbot-response

Bug Fixv0.0.58April 15, 2025

### Fix bug with post\_message\_attachment

Fix an issue with release 0.0.57 where attachments were not made if post\_message\_attachment was called at the end of get\_reponse.

- Fixed issue where attachments weren't created when post\_message\_attachment was called at the end of get\_reponse
- Resolves regression from version 0.0.57

attachmentsbugfixpost-message

Bug Fixv1.0.0March 26, 2025

### Fixed HTML Drag and Drop API issue on Chrome

Fixed an issue preventing the HTML Drag and Drop API from functioning properly on Chrome when users had the chat and canvas displayed side-by-side.

- Fixed HTML Drag and Drop API functionality on Chrome
- Resolved issue with side-by-side chat and canvas display
- Improved drag and drop user experience

canvas-appsdrag-dropchromebugfix

New Featurev0.0.57March 15, 2025

### Support Passing Attachments between Bots

Bots can now pass attachments to each other via fp.stream\_request. OpenAI tool calling improvement included.

- Bots can now pass attachments to each other via fp.stream\_request
- Call post\_message\_attachment function to emit file events to other server bots
- Calling bots receive files in the attachment field of a PartialResponse
- OpenAI tool calling improvement: request finishes without extra unnecessary second call if no tools are decided to be called, saving cost

attachmentsbot-to-botopenaitool-calling

Improvementv1.0.0March 13, 2025

### Better support for Web Workers and WebAssembly libraries

Added better support for libraries that use Web Workers and WebAssembly, making it easier to build more powerful applications with less friction.

- Improved support for Web Workers and WebAssembly libraries
- Libraries now work directly without confirmation prompts
- Supported libraries include Pyodide, PDF.js, and HEIC2any
- Example: Run Python code within canvas apps
- Example: Create apps that analyze PDFs
- Example: Convert HEIC images to standard formats

canvas-appsweb-workerswebassemblypyodidepdf

Improvementv1.0.0March 13, 2025

### Improved UI lag in long chats with App Creator

Improved UI lag in long chats with App Creator via frontend rendering optimizations.

- Reduced UI lag in long chats with App Creator
- Frontend rendering optimizations implemented
- Better performance for extended conversations

canvas-appsui-performancerendering

Improvementv1.0.0March 12, 2025

### App Creator can now incorporate multiple bots by default

App Creator can now incorporate various text, image, video, and audio bots into apps by default without explicit user instruction.

- Text bots: Claude-3.7-Sonnet, GPT-4o, GPT-4o-mini, o3-mini, Gemini-2.0-Flash
- Image bots: FLUX-pro-1.1, FLUX-schnell, remove-background, Bria-Eraser, TopazLabs
- Video bots: Runway, Veo-2
- Audio bots: ElevenLabs, PlayAI-Dialog
- No explicit user instruction required for incorporation

canvas-appsbotsintegrationmultimodal

Improvementv1.0.0March 11, 2025

### Improved App Creator streaming responses

Improved App Creator's ability to stream responses from text bots immediately into the app rather than waiting for the bot response to finish.

- Improved streaming response handling from text bots
- Responses stream immediately into the app
- No longer waits for bot response to finish before displaying
- Better real-time user experience

canvas-appsstreamingreal-time

New Featurev1.0.0March 11, 2025

### Added monthly user counts in Canvas app details

Canvas app details now display monthly user counts for better analytics.

- Monthly user counts now visible in Canvas app details
- Better analytics for app creators
- Improved app performance tracking

canvas-appsanalyticsuser-counts

New Featurev1.0.0March 10, 2025

### Upload images as attachments to App Creator

You can now upload images as attachments directly to App Creator and use them in your app, making it easier to customize your app's design and experience.

- Upload images as attachments directly to App Creator
- Use uploaded images in your app customization
- Easier app design and experience customization
- Direct integration with app development workflow

canvas-appsimage-attachmentscustomization

New Featurev1.0.0March 6, 2025

### Added Game apps category

Added the 'Game apps' category on home page and Explore page.

- New 'Game apps' category added to home page
- Game apps category added to Explore page
- Better organization of gaming-related canvas apps

canvas-appscategoriesgames

Improvementv1.0.0March 4, 2025

### Canvas view default on mobile web

Opening existing chats with canvas on mobile web now displays the canvas view by default, rather than the chat view.

- Canvas view now default when opening existing chats on mobile web
- Previously defaulted to chat view on mobile
- Better mobile user experience for canvas apps

canvas-appsmobiledefault-view

Improvementv1.0.0March 1, 2025

### App Creator now uses vanilla Tailwind CSS by default

App Creator will now use vanilla Tailwind CSS for styling by default, rather than Flowbite.

- Switched from Flowbite to vanilla Tailwind CSS
- Improved output quality, especially for dark mode styling
- Faster app loading speed
- Better default styling approach

canvas-appstailwindcssstyling

Improvementv1.0.0February 28, 2025

### Enabled Claude 3.7 Sonnet thinking capability

Enabled Claude 3.7 Sonnet's 'thinking' capability by default for App Creator to improve performance. The default thinking budget is 4096 tokens.

- Claude 3.7 Sonnet 'thinking' capability enabled by default
- Default thinking budget set to 4096 tokens
- Improved App Creator performance
- Better handling of Markdown responses from bots in created apps

canvas-appsclaude-3.7thinkingperformance

New Featurev1.0.0February 25, 2025

### Canvas Apps & App Creator initial launch on Web

Initial launch of Canvas Apps and App Creator on the web platform.

- Canvas Apps feature launched on web platform
- App Creator tool launched for creating interactive apps
- Full web-based app development environment
- Support for interactive canvas-based applications

canvas-appslaunchweb-platform

New Featurev0.0.56February 15, 2025

### Add DataResponse

This release adds the new DataResponse object which bots can yield to attach a metadata string to their response.

- Added DataResponse object for attaching metadata to responses
- Metadata string can be accessed in the metadata field of associated ProtocolMessage
- Useful for storing additional information about previous messages in conversation

data-responsemetadataprotocol-message

Improvementv0.0.55January 15, 2025

### PDF attachments supported in expand\_text\_attachments

If allow\_attachments and expand\_text\_attachments are both True, PDF files uploaded by the users will have their contents automatically appended to the conversation for the model to reference.

- PDF files now supported in expand\_text\_attachments
- PDF contents automatically appended to conversation when both allow\_attachments and expand\_text\_attachments are True
- Previously only worked for text and html files

pdfattachmentsexpand-text-attachments

Improvementv0.0.54December 15, 2024

### Increased bot dependency limit

Previously, when defining server\_bot\_dependencies there was a limit of 10 calls to other bots for a single message. This limit has been increased to 100 calls for a single message.

- Increased server\_bot\_dependencies limit from 10 to 100 calls per message
- Enables more complex bot interactions and workflows

server-bot-dependencieslimitsbot-calls

Improvementv0.0.53December 15, 2024

### Updated suggested Poe Previews prompt

Updated the suggested optimized Poe Previews prompt to better support React. See https://creator.poe.com/docs/how-to-create-a-prompt-bot#optimize-prompt-for-previews for the full prompt

- Updated Poe Previews prompt with better React support
- Optimized prompt available in documentation
- Improved preview generation capabilities

poe-previewsreactprompt-optimization

Improvementv0.0.52December 15, 2024⚠️ Breaking

### Minimum Python version is now 3.9

We updated the fastapi\_poe library to require Python >=3.9, as Python 3.8 reached end of life in October 2024. This version also includes a fix for tool calls failing when the model decides not to call the function.

- Updated minimum Python version requirement to 3.9
- Python 3.8 reached end of life in October 2024
- Fixed tool calls failing when model decides not to call function

pythonversion-requirementtool-calls

New Featurev0.0.51November 15, 2024

### Support for creating prompt bots in responses

Added ability for server bots to help users create prompt bots with pre-filled fields. See https://creator.poe.com/docs/server-bots-functional-guides#creating-bots-that-help-their-users-create-prompt-bots for more details.

- Server bots can now help users create prompt bots
- Support for pre-filled fields in prompt bot creation
- Detailed documentation available for implementation

prompt-botsserver-botsbot-creation

Improvementv0.0.51November 15, 2024

### Added download\_filename to specify a filename when downloading from url

Added download\_filename for specifying a filename when downloading from url. Previously the filename from the download\_url was always used. This enables bots to set a custom filename for attachments they post via download\_url.

- Added download\_filename parameter for custom filenames
- Previously filename from download\_url was always used
- Enables custom filenames for bot-posted attachments

downloadfilenameattachments

Improvementv0.0.47March 15, 2024

### Expose sync\_bot\_settings

Users can now call sync\_bot\_settings using fp.sync\_bot\_settings() directly

- Exposed sync\_bot\_settings function for direct calling
- Available via fp.sync\_bot\_settings()

syncbot-settingsapi

Improvementv0.0.46January 15, 2024

### ErrorResponse "text" Field is Now User-facing

Prior to this change, the text field of ErrorResponse was not displayed on the client and errors always showed the text "Bot x ran into an unexpected issue". With this change, the text field is now displayed to the user, allowing for custom error messages.

- ErrorResponse text field now displayed to users
- Enables custom error messages instead of generic "Bot x ran into an unexpected issue"
- Recommended to put raw exception in raw\_response field

error-responseuser-facingcustom-messages

New Featurev0.0.45January 15, 2024

### Added sender\_id Field in ProtocolMessage

Added an additional field sender\_id in ProtocolMessage. This is intended to help bot creators differentiate between who sent a particular message, which is useful in a multi-bot chat.

- Added sender\_id field to ProtocolMessage
- Helps differentiate message senders in multi-bot chat
- Useful for bot creators managing multi-bot conversations

protocol-messagesender-idmulti-bot

New Featurev0.0.44January 15, 2024

### Support for Multi Bot Chat

Added enable\_multi\_bot\_chat\_prompting setting and increased bot message timeout from 120s to 600s.

- Added enable\_multi\_bot\_chat\_prompting setting (defaults to False)
- When enabled, Poe combines previous chat history into single message with special prompting
- Provides sufficient context for current bot in multi-bot chat
- Increased bot message timeout from 120s to 600s

multi-botchattimeoutprompting

New Featurev0.0.43December 15, 2023

### Support for Sending Text/Image Attachment Content

Added expand\_text\_attachments and enable\_image\_comprehension settings to request parsed content/descriptions from text and image attachments with the query request.

- Added expand\_text\_attachments setting for parsed text content
- Added enable\_image\_comprehension setting for image descriptions
- Content sent through new parsed\_content field in attachment dictionary
- Makes enabling file uploads much simpler
- Added enforce\_author\_role\_alternation setting for LLM provider compatibility

attachmentstextimagecomprehensionrole-alternation