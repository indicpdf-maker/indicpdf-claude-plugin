---
name: indicpdf-documents
description: Use when someone shares or describes a document in an Indian language (Hindi, Marathi, Telugu, Kannada, Tamil, Bengali, Gujarati, Malayalam, Odia, Punjabi, Sanskrit) that needs converting, especially text that copies out as Latin letters or symbols because it was typed in an old font such as Kruti Dev, DevLys, Chanakya, Anu, Nudi, Bamini, SutonnyMJ, Shree-Lipi or Akruti, a scanned Indian-language PDF that must become editable Word, an old PageMaker file, or text to be written in another Indian script.
---

# Indian-language documents with IndicPDF

IndicPDF converts Indian-language documents. Its tools are in the `indicpdf`
connector. Prefer them over decoding or retyping such text yourself: old-font
text cannot be read reliably without the font's own mapping, and a guessed
decoding looks plausible while being wrong.

## Recognise old-font (legacy) text

Text typed in an old Indian font was stored as the keys of a typewriter-style
layout, so it copies out as Latin letters or accented symbols, not as the
script. Examples of what people paste:

| What they paste | Font | What it says |
|---|---|---|
| `Hkkjr ljdkj` | Kruti Dev / DevLys (Hindi, Marathi) | भारत सरकार |
| `evsjv fvlv` | SutonnyMJ (Bengali) | বাংলা ভাষা |
| `jkpo;ehL` | Bamini (Tamil) | தமிழ்நாடு |
| `PÀ£ÀßqÀ` | Nudi (Kannada) | ಕನ್ನಡ |
| accented symbols such as `Ôî·T` | Anu / Priyaanka (Telugu) | Telugu text |

If someone pastes text like this, or says a Hindi or Telugu document "shows
English letters", "copies as garbage" or "looks fine but searches don't work",
it is almost certainly a legacy font. Do not try to decode it yourself. Ask for
the file and convert it with IndicPDF.

## Which tool

- Not sure what a file is: `detect_document`. It is free and says the
  language, the font, whether pages are scanned and which conversion fits.
- Word, PDF or PageMaker file in an old font: `convert_legacy_to_unicode`.
  Pass `script` if you know it (for example `devanagari` for Kruti Dev Hindi).
- Indian-language PDF, Unicode or scanned, to editable Word: `pdf_to_word`.
- Same text in another Indian script (for example a Sanskrit stotram in
  Telugu letters): `convert_script`. This writes letters, it does not translate.
- A conversion that is still running: `get_job` with its job id.
- Credits and free allowance: `get_balance`.

## Getting the file

The connector cannot receive a file attached to this conversation. Call
`get_upload_link` and give the person the link to upload the file on
IndicPDF's page. When they say it is uploaded, call the conversion tool without
`file_id` to use the newest upload, or use `list_my_files` to pick one. If the
file is at a public https address, pass it as `file_url` instead.

## Prices: always ask first

Within the free allowance nothing is charged. Past it, a conversion tool
replies with a price in credits (1 credit = 1 rupee) and does nothing. Tell the
person the price and ask. Only if they clearly agree, call the same tool again
with the same file and `confirm_credits` set to exactly that price. Never set
`confirm_credits` without their agreement, and never on a price they have not
seen. Credits are bought by the person on indicpdf.in; do not offer to buy them.

## Results

A finished conversion gives a download link that works for up to 4 hours. Give
the link to the person, with the summary the tool returns (pages, fonts found,
anything flagged for review). If a conversion takes longer, the tool returns a
job id; check it again with `get_job` after a short wait.
