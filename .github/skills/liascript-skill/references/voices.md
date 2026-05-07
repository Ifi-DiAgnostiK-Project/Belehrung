# LiaScript Text-to-Speech Voices

Complete reference of available TTS voices for LiaScript narrator comments and inline playback.

## Usage

Set the default voice in the course header:

```markdown
<!--
narrator: US English Female
-->
```

Override per comment or per step:

```markdown
--{{1 Deutsch Male}}--
Dieser Text wird auf Deutsch gesprochen.
```

Inline playback with a specific voice:

```markdown
{!> Russian Female}{Привет}
```

## Voice Table

Blank cells mean that gender is not available. `Nepali` and `Sinhala` have no gender distinction.

| Female                        | Male                        |
| ----------------------------- | --------------------------- |
| UK English Female             | UK English Male             |
| US English Female             | US English Male             |
|                               | Afrikaans Male              |
|                               | Albanian Male               |
| Arabic Female                 | Arabic Male                 |
|                               | Armenian Male               |
| Australian Female             | Australian Male             |
| Bangla Bangladesh Female      | Bangla Bangladesh Male      |
| Bangla India Female           | Bangla India Male           |
|                               | Bosnian Male                |
| Brazilian Portuguese Female   | Brazilian Portuguese Male   |
|                               | Catalan Male                |
| Chinese Female                | Chinese Male                |
| Chinese (Hong Kong) Female    | Chinese (Hong Kong) Male    |
| Chinese Taiwan Female         | Chinese Taiwan Male         |
|                               | Croatian Male               |
| Czech Female                  | Czech Male                  |
| Danish Female                 | Danish Male                 |
| Deutsch Female                | Deutsch Male                |
| Dutch Female                  | Dutch Male                  |
|                               | Esperanto Male              |
|                               | Estonian Male               |
| Filipino Female               |                             |
| Finnish Female                | Finnish Male                |
| French Canadian Female        | French Canadian Male        |
| French Female                 | French Male                 |
| Greek Female                  | Greek Male                  |
| Hindi Female                  | Hindi Male                  |
| Hungarian Female              | Hungarian Male              |
|                               | Icelandic Male              |
| Indonesian Female             | Indonesian Male             |
| Italian Female                | Italian Male                |
| Japanese Female               | Japanese Male               |
| Korean Female                 | Korean Male                 |
| Latin Female                  | Latin Male                  |
|                               | Latvian Male                |
|                               | Macedonian Male             |
| Moldavian Female              | Moldavian Male              |
|                               | Montenegrin Male            |
| Nepali                        | Nepali                      |
| Norwegian Female              | Norwegian Male              |
| Polish Female                 | Polish Male                 |
| Portuguese Female             | Portuguese Male             |
| Romanian Female               | Romanian Male               |
| Russian Female                | Russian Male                |
|                               | Serbian Male                |
|                               | Serbo-Croatian Male         |
| Sinhala                       | Sinhala                     |
| Slovak Female                 | Slovak Male                 |
| Spanish Female                | Spanish Male                |
| Spanish Latin American Female | Spanish Latin American Male |
|                               | Swahili Male                |
| Swedish Female                | Swedish Male                |
| Tamil Female                  | Tamil Male                  |
| Thai Female                   | Thai Male                   |
| Turkish Female                | Turkish Male                |
| Ukrainian Female              |                             |
| Vietnamese Female             | Vietnamese Male             |
|                               | Welsh Male                  |

## Notes

- Use `Deutsch Female/Male` for German — not `German Female/Male`
- Voice availability depends on the user's browser; LiaScript falls back from browser TTS to ResponsiveVoice
- Voice names are case-sensitive
- Quality varies between operating systems and browsers

## Language Codes

Used in the `language:` header field for UI translation and default voice selection:

| Code | Language   |
|------|------------|
| en   | English    |
| de   | German     |
| fr   | French     |
| es   | Spanish    |
| it   | Italian    |
| pt   | Portuguese |
| nl   | Dutch      |
| pl   | Polish     |
| ru   | Russian    |
| zh   | Chinese    |
| ja   | Japanese   |
| ko   | Korean     |
| ar   | Arabic     |
| hi   | Hindi      |
| tr   | Turkish    |
| uk   | Ukrainian  |
