
# SQLZOO solutions

I’ve just completed the sixth course in the Google Data Analytics program and wanted to sharpen my SQL skills before moving on to R.
This repository contains my solutions and notes from working through the SQLZOO challenges.

## Table of Contents

- [0 SELECT basics](#select-basics)
- [1 SELECT name](#select-name)
- [2 SELECT from World](#select-from-world)
- [3 SELECT from Nobel](#select-from-nobel)
- [4 SELECT within SELECT](#select-within-select)
- [5 SUM and COUNT](#sum-and-count)
- [6 JOIN](#join)
- [7 More JOIN operations](#more-join-operations)
- [8 Using Null](#using-null)
- [9 Self join](#self-join)

### SELECT basics
"Apt." is a song by New Zealand and South Korean singer Rosé and American musician Bruno Mars. It was released through the Black Label and Atlantic Records on 18 October 2024, as the lead single from Rosé's debut studio album, Rosie (2024). "Apt." marked Rosé's first solo single in three years and her first release since departing from YG Entertainment and Interscope Records in 2023. The song was written and composed by various contributors, including Rosé and Mars, and includes elements from the 1982 tune "Mickey" by Toni Basil. It is an up-tempo pop, pop rock, pop-punk, and new wave track, featuring indie rock and electropop influences. Inspired by a South Korean drinking game, the song's chorus is built around the game's rhythmic chant of apateu (Korean: 아파트; lit. apartment; pronounced [a̠pʰa̠tʰɯ]).

Critics lauded "Apt." for its catchy production, broad cross-cultural appeal, and its role in promoting Korean culture worldwide. It was a commercial success and spent 12 weeks atop the Billboard Global 200, becoming Rosé and Mars' second number-one single each and the longest-running number-one song of 2024. In South Korea, it peaked at number one on the Circle Digital Chart for 10 weeks. "Apt." was the first song by a K-pop female soloist to top Australia's ARIA Singles Chart and the first Western song to top the Billboard Japan Hot 100 in over a decade. The song saw huge global success, topping the charts in over 50 countries including Austria, Belgium, Canada, Germany, Indonesia, New Zealand, Norway, the Philippines, Sweden, Switzerland and Taiwan. It entered the top three on the US Billboard Hot 100 and the UK Singles Chart, the first song by a K-pop female act to do so on either.

An accompanying music video was directed by Mars and Daniel Ramos and premiered on Rosé's YouTube channel simultaneously with the single's release. The video featured Rosé and Mars as a garage band with matching black leather jackets in a pink-coloured set. The song broke a number of viewership records on YouTube, becoming the fastest music video by an Asian act to reach one billion views on the platform. "Apt." was also the second-fastest song and the fastest by a K-pop artist to reach one billion streams in Spotify history. Rosé promoted the song with performances on The Seasons: Lee Young-ji's Rainbow, BBC Radio 1's Christmas Live Lounge 2024, and The Tonight Show Starring Jimmy Fallon. She performed it with Mars at the 2024 MAMA Awards, where they received the Global Sensation award.

Background and promotion
On 29 December 2023, Rosé announced her departure from YG Entertainment to its associate company The Black Label for her solo work, while remaining with YG to continue her activities as a member of Blackpink. Prior to her departure, Rosé released her debut solo single album, R, in March 2021, featuring the songs "On the Ground" and "Gone". These releases garnered commercial success.[2][3]

In August 2024, Rosé was seen attending a concert of Bruno Mars in Los Angeles, later sharing a picture of her wearing a shirt with Mars on it.[4] In September, Rosé announced via her social media that she signed a new global solo deal with Atlantic Records.[3] On 16 October, Rosé posted a polaroid picture of her sitting next to Mars and revealed that she taught him a Korean drinking game.[5] Mars also shared an Instagram story of Rosé supposedly trying to kiss him that night, promoting a possible upcoming release.[6]

On 17 October, Rosé announced the release of the single on her social media, a day ahead of the release.[7] An accompanying artwork was revealed alongside the announcement, featuring a black-and-white rose-tinted photo of Mars behind a drum set and Rosé lying in front of the set wearing a black leather jacket and skirt.[8] The news of the release arrived a few weeks after the announcement of Rosé's debut studio album Rosie, slated for release on 6 December 2024.[9]

Composition and lyrics

"Apt."
Duration: 16 seconds.0:16
Inspired by the apateu rhythmic chant of a South Korean drinking game, the song's chorus received praise for its catchiness and energetic sound.
Problems playing this file? See media help.
"Apt." was written by Rosé, Amy Allen, Brody Brown, Philip Lawrence, Theron Thomas of R. City, Rogét Chahayed, Omer Fedi, Cirkut, and Mars, while being produced by the latter four; additional writing credits go to Nicky Chinn and Mike Chapman for the interpolation of Toni Basil's 1982 single "Mickey".[10] "Apt." has been described as a pop,[11] pop-punk,[12] pop rock,[13] and new wave track,[14] featuring indie rock and electropop elements.[11] It opens with a rap verse, transitions to a "melodious" pre-chorus, and builds to an energetic chorus influenced by the Apartment game chant.[15]

'APT' is actually my favourite Korean drinking game that I play with my friends back home. It's so simple, puts a smile on your face, and breaks the ice at any party. One night in the studio, I taught my crew how to play the game. Everyone was fascinated, especially when I started the chant, so we played around with it, and I said we should make a song out of it... and after Bruno joined the track, the rest became history!

— Rosé on the song's origins.[16]





















### SELECT name
"Apt." is a song by New Zealand and South Korean singer Rosé and American musician Bruno Mars. It was released through the Black Label and Atlantic Records on 18 October 2024, as the lead single from Rosé's debut studio album, Rosie (2024). "Apt." marked Rosé's first solo single in three years and her first release since departing from YG Entertainment and Interscope Records in 2023. The song was written and composed by various contributors, including Rosé and Mars, and includes elements from the 1982 tune "Mickey" by Toni Basil. It is an up-tempo pop, pop rock, pop-punk, and new wave track, featuring indie rock and electropop influences. Inspired by a South Korean drinking game, the song's chorus is built around the game's rhythmic chant of apateu (Korean: 아파트; lit. apartment; pronounced [a̠pʰa̠tʰɯ]).

Critics lauded "Apt." for its catchy production, broad cross-cultural appeal, and its role in promoting Korean culture worldwide. It was a commercial success and spent 12 weeks atop the Billboard Global 200, becoming Rosé and Mars' second number-one single each and the longest-running number-one song of 2024. In South Korea, it peaked at number one on the Circle Digital Chart for 10 weeks. "Apt." was the first song by a K-pop female soloist to top Australia's ARIA Singles Chart and the first Western song to top the Billboard Japan Hot 100 in over a decade. The song saw huge global success, topping the charts in over 50 countries including Austria, Belgium, Canada, Germany, Indonesia, New Zealand, Norway, the Philippines, Sweden, Switzerland and Taiwan. It entered the top three on the US Billboard Hot 100 and the UK Singles Chart, the first song by a K-pop female act to do so on either.

An accompanying music video was directed by Mars and Daniel Ramos and premiered on Rosé's YouTube channel simultaneously with the single's release. The video featured Rosé and Mars as a garage band with matching black leather jackets in a pink-coloured set. The song broke a number of viewership records on YouTube, becoming the fastest music video by an Asian act to reach one billion views on the platform. "Apt." was also the second-fastest song and the fastest by a K-pop artist to reach one billion streams in Spotify history. Rosé promoted the song with performances on The Seasons: Lee Young-ji's Rainbow, BBC Radio 1's Christmas Live Lounge 2024, and The Tonight Show Starring Jimmy Fallon. She performed it with Mars at the 2024 MAMA Awards, where they received the Global Sensation award.

Background and promotion
On 29 December 2023, Rosé announced her departure from YG Entertainment to its associate company The Black Label for her solo work, while remaining with YG to continue her activities as a member of Blackpink. Prior to her departure, Rosé released her debut solo single album, R, in March 2021, featuring the songs "On the Ground" and "Gone". These releases garnered commercial success.[2][3]

In August 2024, Rosé was seen attending a concert of Bruno Mars in Los Angeles, later sharing a picture of her wearing a shirt with Mars on it.[4] In September, Rosé announced via her social media that she signed a new global solo deal with Atlantic Records.[3] On 16 October, Rosé posted a polaroid picture of her sitting next to Mars and revealed that she taught him a Korean drinking game.[5] Mars also shared an Instagram story of Rosé supposedly trying to kiss him that night, promoting a possible upcoming release.[6]

On 17 October, Rosé announced the release of the single on her social media, a day ahead of the release.[7] An accompanying artwork was revealed alongside the announcement, featuring a black-and-white rose-tinted photo of Mars behind a drum set and Rosé lying in front of the set wearing a black leather jacket and skirt.[8] The news of the release arrived a few weeks after the announcement of Rosé's debut studio album Rosie, slated for release on 6 December 2024.[9]

Composition and lyrics

"Apt."
Duration: 16 seconds.0:16
Inspired by the apateu rhythmic chant of a South Korean drinking game, the song's chorus received praise for its catchiness and energetic sound.
Problems playing this file? See media help.
"Apt." was written by Rosé, Amy Allen, Brody Brown, Philip Lawrence, Theron Thomas of R. City, Rogét Chahayed, Omer Fedi, Cirkut, and Mars, while being produced by the latter four; additional writing credits go to Nicky Chinn and Mike Chapman for the interpolation of Toni Basil's 1982 single "Mickey".[10] "Apt." has been described as a pop,[11] pop-punk,[12] pop rock,[13] and new wave track,[14] featuring indie rock and electropop elements.[11] It opens with a rap verse, transitions to a "melodious" pre-chorus, and builds to an energetic chorus influenced by the Apartment game chant.[15]

'APT' is actually my favourite Korean drinking game that I play with my friends back home. It's so simple, puts a smile on your face, and breaks the ice at any party. One night in the studio, I taught my crew how to play the game. Everyone was fascinated, especially when I started the chant, so we played around with it, and I said we should make a song out of it... and after Bruno joined the track, the rest became history!

— Rosé on the song's origins.[16]


















### SELECT from World
"Apt." is a song by New Zealand and South Korean singer Rosé and American musician Bruno Mars. It was released through the Black Label and Atlantic Records on 18 October 2024, as the lead single from Rosé's debut studio album, Rosie (2024). "Apt." marked Rosé's first solo single in three years and her first release since departing from YG Entertainment and Interscope Records in 2023. The song was written and composed by various contributors, including Rosé and Mars, and includes elements from the 1982 tune "Mickey" by Toni Basil. It is an up-tempo pop, pop rock, pop-punk, and new wave track, featuring indie rock and electropop influences. Inspired by a South Korean drinking game, the song's chorus is built around the game's rhythmic chant of apateu (Korean: 아파트; lit. apartment; pronounced [a̠pʰa̠tʰɯ]).

Critics lauded "Apt." for its catchy production, broad cross-cultural appeal, and its role in promoting Korean culture worldwide. It was a commercial success and spent 12 weeks atop the Billboard Global 200, becoming Rosé and Mars' second number-one single each and the longest-running number-one song of 2024. In South Korea, it peaked at number one on the Circle Digital Chart for 10 weeks. "Apt." was the first song by a K-pop female soloist to top Australia's ARIA Singles Chart and the first Western song to top the Billboard Japan Hot 100 in over a decade. The song saw huge global success, topping the charts in over 50 countries including Austria, Belgium, Canada, Germany, Indonesia, New Zealand, Norway, the Philippines, Sweden, Switzerland and Taiwan. It entered the top three on the US Billboard Hot 100 and the UK Singles Chart, the first song by a K-pop female act to do so on either.

An accompanying music video was directed by Mars and Daniel Ramos and premiered on Rosé's YouTube channel simultaneously with the single's release. The video featured Rosé and Mars as a garage band with matching black leather jackets in a pink-coloured set. The song broke a number of viewership records on YouTube, becoming the fastest music video by an Asian act to reach one billion views on the platform. "Apt." was also the second-fastest song and the fastest by a K-pop artist to reach one billion streams in Spotify history. Rosé promoted the song with performances on The Seasons: Lee Young-ji's Rainbow, BBC Radio 1's Christmas Live Lounge 2024, and The Tonight Show Starring Jimmy Fallon. She performed it with Mars at the 2024 MAMA Awards, where they received the Global Sensation award.

Background and promotion
On 29 December 2023, Rosé announced her departure from YG Entertainment to its associate company The Black Label for her solo work, while remaining with YG to continue her activities as a member of Blackpink. Prior to her departure, Rosé released her debut solo single album, R, in March 2021, featuring the songs "On the Ground" and "Gone". These releases garnered commercial success.[2][3]

In August 2024, Rosé was seen attending a concert of Bruno Mars in Los Angeles, later sharing a picture of her wearing a shirt with Mars on it.[4] In September, Rosé announced via her social media that she signed a new global solo deal with Atlantic Records.[3] On 16 October, Rosé posted a polaroid picture of her sitting next to Mars and revealed that she taught him a Korean drinking game.[5] Mars also shared an Instagram story of Rosé supposedly trying to kiss him that night, promoting a possible upcoming release.[6]

On 17 October, Rosé announced the release of the single on her social media, a day ahead of the release.[7] An accompanying artwork was revealed alongside the announcement, featuring a black-and-white rose-tinted photo of Mars behind a drum set and Rosé lying in front of the set wearing a black leather jacket and skirt.[8] The news of the release arrived a few weeks after the announcement of Rosé's debut studio album Rosie, slated for release on 6 December 2024.[9]

Composition and lyrics

"Apt."
Duration: 16 seconds.0:16
Inspired by the apateu rhythmic chant of a South Korean drinking game, the song's chorus received praise for its catchiness and energetic sound.
Problems playing this file? See media help.
"Apt." was written by Rosé, Amy Allen, Brody Brown, Philip Lawrence, Theron Thomas of R. City, Rogét Chahayed, Omer Fedi, Cirkut, and Mars, while being produced by the latter four; additional writing credits go to Nicky Chinn and Mike Chapman for the interpolation of Toni Basil's 1982 single "Mickey".[10] "Apt." has been described as a pop,[11] pop-punk,[12] pop rock,[13] and new wave track,[14] featuring indie rock and electropop elements.[11] It opens with a rap verse, transitions to a "melodious" pre-chorus, and builds to an energetic chorus influenced by the Apartment game chant.[15]

'APT' is actually my favourite Korean drinking game that I play with my friends back home. It's so simple, puts a smile on your face, and breaks the ice at any party. One night in the studio, I taught my crew how to play the game. Everyone was fascinated, especially when I started the chant, so we played around with it, and I said we should make a song out of it... and after Bruno joined the track, the rest became history!

— Rosé on the song's origins.[16]
...



