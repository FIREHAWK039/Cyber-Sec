We learned that ASCII is a 7-bit standard that defines 128 characters covering English letters, digits, and basic punctuation. We also noticed how ASCII, with its seven bits, didn’t have room for characters such as `ñ`, `€`, `あ`, or `ب`. Using eight bits, extended ASCII tried patching this with regional variants (ISO-8859-1, ISO-8859-2, Windows-1252, among many others), but this caused chaos! For example, if the sender writes and saves `Ø` using ISO 8859-1 (Latin 1) encoding and the recipient opens and reads the document using ISO 8859-2 (Latin 2) encoding, they will see `Ř`. Hence, it is clear how opening a document requires us to use the same encoding used when saving it; otherwise, various characters will not be displayed correctly, or even more confusingly, they might be incorrectly replaced.

Unlike English, which has 26 letters and needs **52 characters** to cover upper-case and lower-case letters, Arabic needs more than **250 characters** to cover its various ligatures and diacritics. Moreover, the number escalates rapidly when considering Japanese and Chinese. In Japanese, 2,136 Kanji (logographic characters) are considered daily-use characters, as mandated by Japan’s Ministry of Education. In fact, the **JIS X 0208** standard defines **6,879 characters**. In Chinese, educated natives recognize around 8,000 characters. Furthermore, the **GB 18030-2022** defines more than **87,887 Hanzi (Chinese characters)**. And still, we have not considered encoding emoticons (emoji).

In other words, it is essential for both the sender and the recipient to use the same encoding; moreover, we need an encoding that can include all the characters from all languages. This situation brings us to Unicode.

Unicode is a universal character encoding standard. It assigns unique code points to characters from all modern and historical writing systems worldwide. Unicode supports the interchange, processing, and display of text in diverse languages. In other words, we don’t need to worry about picking a specific encoding standard that is compatible with the language we are using. Furthermore, this makes it easy to use different languages in a single file or message. And most importantly, because this is a standard that fits all, we don’t need to worry about the encoding used by the original author, as they will also be using Unicode.

Unicode is a character set standard that assigns a unique number to every character across all languages. Examples:

- U+0041 = Latin “A”
- U+03A9 = Greek “Ω”
- U+3042 = Japanese Hiragana “あ”

Unicode 17.0 is currently the latest version of the [Unicode(opens in new tab)](https://home.unicode.org/) Standard. It defines close to **157 thousand** characters, almost **4,000** of them are emoji sequences.

## UTF-8, UTF-16, and UTF-32

Because you will encounter UTF-8, UTF-16, and UTF-32, we will briefly cover them without going into too much depth. What you need to know is that UTF-8 is very common on the modern web. It encodes Unicode points into 1 to 4 bytes dynamically. In other words, it decides on the number of bytes based on the character complexity. ASCII characters (`U+0000` to `U+007F`) use exactly 1 byte, identical to the original ASCII, ensuring seamless backward compatibility. Non-ASCII characters like Ω (`U+03A9`) use 2 bytes, while complex scripts or emoji like 🔥 (`U+1F525`) require 4 bytes. This flexibility allows us to cover the Unicode standard without wasting bytes.

UTF-16 takes a different path; it uses either 2 or 4 bytes per character. Common characters, like most Latin, Cyrillic, or Chinese Hanzi, fit in 2 bytes; however, rarer ones, like emoji or ancient scripts, require a pair, i.e., two 16-bit units totaling 4 bytes. For example, the letter `A` is encoded as `U+0041`, while the emoji 🔥 needs two and is encoded as `U+D83D U+DD25`.

Finally, UTF-32 is the simplest but also the most wasteful; every Unicode code point uses exactly 4 bytes. For example, `A` is encoded as `U+00000041` and 🔥 is encoded as `U+0001F525`.

Let’s explore a few more examples:

- 龍: One of the Chinese characters that appear on offensive Linux distributions, such as Kali, is “龍”, which means “dragon”. In Unicode, it is `U+9F8D` or `U+00009F8D`, depending on whether it is UTF-16 or UTF-32.
- 😊: This smiley face is nothing more than `U+0001F60A` in UTF-32 for a computer; that’s literally `0000 0000 0000 0001 1111 0110 0000 1010`.
- ツ: The Japanese letter “tsu” which some people use as a smiley face in some regions outside Japan; it has the code U+30C4 or U+000030C4 depending on whether it is UTF-16 or UTF-32.
- ت is the Arabic letter “taa,” and some people use it as a smiley outside the Arab world; it looks close enough to a smiley face. From a Unicode perspective, that’s `U+062A`.
- ♞: The black knight in chess uses the Unicode `U+265E`; in other words, the computer reads `0010 0110 0101 1110` and shows you a black knight, thanks to Unicode