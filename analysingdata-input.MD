1. qid
qid = [question ID (问题ID)]
string · lengths = [string (字符串) · lengths (长度)]
Meaning: A 6-character string used as a unique identifier.
中文: qid 是一个6位的字符串，代表问题的唯一ID。
2. video_id
video_id = [video ID (视频ID)]
string · classes = [string (字符串) · classes (类别)]
Meaning: A string that serves as an ID for a video, with 289 unique IDs detected (categorical).
中文: 视频的ID，具有 289 个不同的类别。
3. question_type
question_type = [question type (问题类型)]
string · classes = [string (字符串) · classes (类别)]
Meaning: Categorical field with 5 distinct types of questions.
中文: 问题的类型，具有 5 个不同的类别。
4. capability
capability = [capability (能力/技能)]
string · classes = [string (字符串) · classes (类别)]
Meaning: Describes the capability tested by the question (e.g., "temporal reasoning"). 18 unique values.
中文: 描述问题考察的能力，有 18 个不同的类别。
5. question
question = [question text (问题文本)]
string · lengths = [string (字符串) · lengths (长度)]
Meaning: The full text of the question, length varies (17-373 characters).
中文: 实际问题内容，长度范围从 17 到 373 个字符。
6. duration
duration = [video duration (视频时长)]
string · classes = [string (字符串) · classes (类别)]
Meaning: Duration of the video, stored as a string, with 254 different values detected.
中文: 视频的时长，有 254 个不同的类别（时长值）。
7. question_prompt
question_prompt = [question prompt (问题提示/提示词)]
string · classes = [string (字符串) · classes (类别)]
Meaning: Likely a binary field (e.g., Yes/No or True/False) indicating whether a question prompt is provided.
中文: 是否有提示的字段，有 2 个不同的值。
8. answer
answer = [answer (答案)]
string · classes = [string (字符串) · classes (类别)]
Meaning: The answer to the question; currently, only 1 class detected.
中文: 正确答案，目前只有 1 个类别。
9. youtube_url
youtube_url = [YouTube URL (YouTube链接)]
string · classes = [string (字符串) · classes (类别)]
Meaning: URL to the related YouTube video, with 292 unique URLs found.
中文: 相关 YouTube 视频的链接，有 292 个不同的链接。


# These are the features
qid	video_id	question_type	capability	question	duration	question_prompt	answer	youtube_url

question we dont have to take into account

question_type we have to take into account
duration do we havet ot?

# Some queries I have. They provided the videos so measn we can use a snip the video

