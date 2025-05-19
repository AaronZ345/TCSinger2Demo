

{:.no_toc}
* toc
{:toc}


# Abstract

Customizable multilingual zero-shot singing voice synthesis (SVS) has various potential applications in music composition and short video dubbing. However, existing SVS models overly depend on phoneme and note boundary annotations, limiting their robustness in zero-shot scenarios and producing poor transitions between phonemes and notes. Moreover, they also lack effective multi-level style control via diverse prompts. To overcome these challenges, we introduce TCSinger 2, a multi-task multilingual zero-shot SVS model with style transfer and style control based on various prompts. TCSinger 2 mainly includes three key modules: 1) Blurred Boundary Content (BBC) Encoder, predicts duration, extends content embedding, and applies masking to the boundaries to enable smooth transitions.2) Custom Audio Encoder, uses contrastive learning to extract aligned representations from singing, speech, and textual prompts.3) Flow-based Custom Transformer, leverages Cus-MOE, with F0 supervision, enhancing both the synthesis quality and style modeling of the generated singing voice. Experimental results show that  outperforms baseline models in both subjective and objective metrics across multiple related tasks. 

---

**Note：** We conduct all tasks in the zero-shot scenario, with training and testing on multi-lingual speech and singing data. All samples are resample to 48kHZ.

---

# Style Transfer

## Parallel Style Transfer

For the parallel experiments, we randomly select samples with unseen singers from the test set as target voices and use different utterances from the same singers to form prompts. We also input music scores as contents.

1.**Target Lyric:** 回忆里想起模糊的小时候，云朵漂浮在蓝蓝的天空

**Language:** Chinese

Successfully transferred timbre, accent, enunciation, pop singing method, emotion.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>StyleTTS 2</th>
		<th style='text-align: center'>CosyVoice</th>
			<th style='text-align: center'>VISinger 2</th>
			<th style='text-align: center'>TCSinger</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/style/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cosy/002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/vi/002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/tc/002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cus/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>


2.**Target Lyric:** 入夜渐微凉，繁花落地成霜，你在远方眺望，耗尽所有暮光，不思量

**Language:** Chinese

Successfully transferred timbre, accent, enunciation, pop singing method.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>StyleTTS 2</th>
		<th style='text-align: center'>CosyVoice</th>
			<th style='text-align: center'>VISinger 2</th>
			<th style='text-align: center'>TCSinger</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/style/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cosy/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/vi/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/tc/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cus/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

3.**Target Lyric:** how to be brave,how can I love when I'm afraid

**Langugae:** English

Successfully transferred timbre, accent, enunciation, pop singing method, and mixed voice technique.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/003.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>StyleTTS 2</th>
		<th style='text-align: center'>CosyVoice</th>
			<th style='text-align: center'>VISinger 2</th>
			<th style='text-align: center'>TCSinger</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/style/003.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cosy/003.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/vi/003.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/tc/003.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cus/003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

4.**Target Lyric:** allons, en garde, allons, allons, ah toréador

**Language:** French

Successfully transferred timbre, accent, enunciation, bel canto singing method.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/004.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>StyleTTS 2</th>
		<th style='text-align: center'>CosyVoice</th>
			<th style='text-align: center'>VISinger 2</th>
			<th style='text-align: center'>TCSinger</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/style/004.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cosy/004.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/vi/004.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/tc/004.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/cus/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

## Cross-lingual Style Transfer

Additionally, we utilize unseen test data with different lyric languages (such as English and Chinese) as prompts and targets for inference. We also input music scores as contents.

1.**Target Lyric:** 在我的怀里，在你的眼里

**Language:** From English to Chinese

Successfully transferred timbre, accent, enunciation, pop singing method.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/cross/prompt/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/cross/cus/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>


2.**Target Lyric:** or do you need more, is there something you're searching

**Language:** From Japanese to English

Successfully transferred timbre, accent, enunciation, pop singing method.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/cross/prompt/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/cross/cus/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

## Non-parallel Style Transfer

Additionally, we employ unseen test data with different styles to generate the same content in entirely distinct ways from the original version. We also use music scores as input content.

It is evident that the timbre, accent, and enunciation have been successfully transferred. In addition, the first example successfully transfers the emotional expression of the singing, the second captures the falsetto technique, and the third reproduces the breathy technique.

**Target Lyric:** 雨到了这里缠成线，缠着我们流连人世间

**Language:** Chinese

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt Audio</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unst/prompt/003.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unst/cus/003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unst/prompt/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unst/cus/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unst/prompt/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unst/cus/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

---

# Style Control

Multi-level styles are randomly assigned in a manner that is appropriate for the context. These styles include global timbre (such as the singer's gender and vocal range), singing method (e.g., bel canto and pop), emotion (e.g., happy and sad), and segment-level or word-level techniques (such as mixed voice, falsetto, breathy, vibrato, glissando, and pharyngeal). We also input the same music scores as content.

**Target Lyric:** 一壶清酒一生尘灰

**Language:** Chinese

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Textual Prompt</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th style='text-align: center; font-weight: normal;'>A female singer with an alto vocal range performs a pop song.</th>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unsc/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
	<tbody>
		<tr>
			<th style='text-align: center; font-weight: normal;'>A male singer with an tenor vocal range performs a pop song.</th>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unsc/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
	<tbody>
		<tr>
			<th style='text-align: center; font-weight: normal;'>A female singer with an alto vocal range performs a pop song. She sings with the breathy technique in the whole segment.</th>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unsc/003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
	<tbody>
		<tr>
			<th style='text-align: center; font-weight: normal;'>A female singer with an alto vocal range performs a pop song. She begins with the breathy techniques in the first half of the song (three words), before transitioning into falsetto for the second half (about five words).</th>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/unsc/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

---

# Speech-to-Singing Style Transfer

We randomly select unseen singers from the test set as target samples and different speech samples from the same singers to form the prompts. We also input music scores as contents.

1.**Target Lyric:** 风到这里就是粘，粘住过客的思念

**Language:** Chinese

Successfully transferred timbre, accent, enunciation.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/prompt/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/cus/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>


2.**Target Lyric:** Anytime you whisper my name, you'll see

**Language:** English

Successfully transferred timbre, accent, enunciation.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/prompt/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/cus/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>


3.**Target Lyric:** parais, astre pur, et charmant

**Language:** French

Successfully transferred timbre, accent, enunciation.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/prompt/003.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/cus/003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>


4.**Target Lyric:** господи, как это, господи, как это,
как это больно

**Language:** Russian

Successfully transferred timbre, accent, enunciation.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>TCSinger 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/prompt/004.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/sts/cus/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>
