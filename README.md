第1步：在项目目录中创建一个数据文件夹，下载
康奈尔电影对话语料库来自
https://www.cs.cornell.edu/~cristian/Cornell_Movie-Dialogs_Corpus.html
解压缩它

第2步：更新config.py配置文件中的DATA_PATH 参数
将DATA_PATH更改为实际存储数据的位置

第3步：运行 python3 data.py 对数据进行数据预处理
这将对Cornell数据集进行所有预处理，生成processed 文件夹
里面生成很多10个文件

第4步：
python3 chatbot.py --mode [train / chat]

如果模式是train，那么你训练聊天机器人。 默认情况下，模型会
恢复以前训练过的模型（如果有的话）并继续
对此进行训练。

如果您想从头开始培训，请删除所有checkpoint下的内容
在检查点文件夹中。

如果模式是聊天，您将进入与机器人的交互模式。

默认情况下，您将使用聊天机器人进行所有对话
进入已处理文件夹中的文件output_convo.txt。 如果你运行这个聊天机器人，



A neural chatbot using sequence to sequence model with
attentional decoder. This is a fully functional chatbot.

This is based on Google Translate Tensorflow model
https://github.com/tensorflow/models/blob/master/tutorials/rnn/translate/

Sequence to sequence model by Cho et al.(2014)

Created by Chip Huyen (chiphuyen@cs.stanford.edu)
CS20: "TensorFlow for Deep Learning Research"
cs20.stanford.edu

The detailed assignment handout can be found at:
https://docs.google.com/document/d/1GJfn2B6EI8JueDiBwzTAdD34d6pC99BSt6vldOmUCPQ/edit?usp=sharing


<h2>Sample conversation</h2>
HUMAN ++++ hi <br>
BOT ++++ hi . what ' s your name ?<br>
HUMAN ++++ i'm chip<br>
BOT ++++ please .<br>
HUMAN ++++ please what?<br>
BOT ++++ i don ' t know what to say .<br>
HUMAN ++++ where are you from?<br>
BOT ++++ california .<br>
HUMAN ++++ do you like california?<br>
BOT ++++ i ' m okay .<br>
HUMAN ++++ i like california a lot<br>
BOT ++++ of what ?<br>
HUMAN ++++ i live here<br>
BOT ++++ and what is it ?<br>
HUMAN ++++ california<br>
BOT ++++ i don ' t know what to say .<br>
HUMAN ++++ i'm a student here<br>
BOT ++++ and get it out of here .<br>
HUMAN ++++ what do you like to do in your free time?<br>
BOT ++++ and what about the gun ?<br>
HUMAN ++++ do you have a gun?<br>
BOT ++++ yes .<br>
HUMAN ++++ you're dangerous!<br>
BOT ++++ i ' m not .<br>
HUMAN ++++ do you go hunting?<br>
BOT ++++ i can do .<br>
HUMAN ++++ what do you hunt?<br>
BOT ++++ virgin .<br>
HUMAN ++++ that's very bad<br>
BOT ++++ and you in love ?<br>
HUMAN ++++ no i'm not<br>
BOT ++++ please - -<br>
HUMAN ++++ okay, i am<br>
BOT ++++ and you are good .<br>
HUMAN ++++ yeah i am good too.<br>
BOT ++++ good good to you .<br>
HUMAN ++++ are you in love?<br>
BOT ++++ i ' m ready .<br>
HUMAN ++++ ready for what?<br>
BOT ++++ for what ?<br>
HUMAN ++++ for what?<br>
BOT ++++ i don ' t know what to say .<br>
HUMAN ++++ tell me<br>
BOT ++++ i can do it .<br>
HUMAN ++++ okay, tell me what you're ready for<br>
BOT ++++ i ' m doing you .<br>
HUMAN ++++ no you're not<br>
BOT ++++ please !<br>
HUMAN ++++ this is a strange conversation<br>
BOT ++++ i don ' t know what to say .<br>
HUMAN ++++ are you a guy?<br>
BOT ++++ of what ?<br>
HUMAN ++++ are you a boy?<br>
BOT ++++ i ' m fine .<br>
HUMAN ++++ are you a man?<br>
BOT ++++ i ' m a little .<br>
HUMAN ++++ what's your name?<br>
BOT ++++ chris -<br>
HUMAN ++++ chris who?<br>
BOT ++++ cornelius .<br>
HUMAN ++++ so i guess you're a guy.<br>
BOT ++++ i am .<br>
HUMAN ++++ okay<br>
BOT ++++ okay ?<br>
HUMAN ++++ do you have a girlfriend?<br>
BOT ++++ i ' m sure .<br>
HUMAN ++++ what's her name?<br>
BOT ++++ let ' s talk about something else .<br>

See output_convo.txt for more sample conversations.

<h2>Usage</h2>

Step 1: create a data folder in your project directory, download
the Cornell Movie-Dialogs Corpus from
https://www.cs.cornell.edu/~cristian/Cornell_Movie-Dialogs_Corpus.html
Unzip it

Step 2: update config.py file<br>
Change DATA_PATH to where you store your data

Step 3: python3 data.py<br>
This will do all the pre-processing for the Cornell dataset.

Step 4:
python3 chatbot.py --mode [train/chat] <br>
If mode is train, then you train the chatbot. By default, the model will
restore the previously trained weights (if there is any) and continue
training up on that.

If you want to start training from scratch, please delete all the checkpoints
in the checkpoints folder.

If the mode is chat, you'll go into the interaction mode with the bot.

By default, all the conversations you have with the chatbot will be written
into the file output_convo.txt in the processed folder. If you run this chatbot,
I kindly ask you to send me the output_convo.txt so that I can improve
the chatbot.


Thank you very much!

康奈尔大学的电影对白语料库介绍


- movie_titles_metadata.txt

数据集结果解释：
    1所有文件以" +++$+++ "分隔符
    - 包含每部电影标题信息
        - fields:
            - movieID, 电影id
            - movie title, 电影标题
            - movie year,  电影年份
               - IMDB rating, IMDB评分
            - no. IMDB votes, IMDB 投票
             - genres in the format ['genre1','genre2',?'genreN'] 电影类型

例子：m25 +++$+++ backdraft +++$+++ 1991 +++$+++ 6.60 +++$+++ 28541 +++$+++ ['action', 'crime', 'drama', 'mystery', 'thriller']

 电影id m25  电影标题：backdraft 电影年份：1991 评分 6.60  总投票次数：28541 电影类型： 动作，犯罪，。。。。




 - movie_characters_metadata.txt
     - 包含每部电影角色信息
     - fields:
         - characterID
         - character name
         - movieID
         - movie title
         - gender ("?" for unlabeled cases)
         - position in credits ("?" for unlabeled cases)


 关键是下面两个文件，一个包含了所有文本，一个包含了文本之间的关系


 - movie_lines.txt
     - 包含每个表达(utterance)的实际文本
     - fields:
         - lineID
         - characterID (who uttered this phrase)
         - movieID
         - character name
         - text of the utterance

 前面5个样本:

 L1045 +++$+++ u0 +++$+++ m0 +++$+++ BIANCA +++$+++ They do not!
 L1044 +++$+++ u2 +++$+++ m0 +++$+++ CAMERON +++$+++ They do to!
 L985 +++$+++ u0 +++$+++ m0 +++$+++ BIANCA +++$+++ I hope so.
 L984 +++$+++ u2 +++$+++ m0 +++$+++ CAMERON +++$+++ She okay?
 L925 +++$+++ u0 +++$+++ m0 +++$+++ BIANCA +++$+++ Let's go.
 ---------------------


- movie_conversations.txt
    - 对话的结构-
    - fields
        - characterID of the first character involved in the conversation 对话中的第一个角色的ID

        - characterID of the second character involved in the conversation 对话中的第二个角色的ID

        - movieID of the movie in which the conversation occurred  对话所属电影的ID


        - list of the utterances that make the conversation, in chronological
            order: ['lineID1','lineID2',?'lineIDN']
            has to be matched with movie_lines.txt to reconstruct the actual content

            对话中以时间顺序的各个表达的列表，

           order: ['lineID1','lineID2',?'lineIDN']必须和movie_lines.txt匹配以便于重构实际内容

前面5个样本:

u0 +++$+++ u2 +++$+++ m0 +++$+++ ['L194', 'L195', 'L196', 'L197']
u0 +++$+++ u2 +++$+++ m0 +++$+++ ['L198', 'L199']
u0 +++$+++ u2 +++$+++ m0 +++$+++ ['L200', 'L201', 'L202', 'L203']
u0 +++$+++ u2 +++$+++ m0 +++$+++ ['L204', 'L205', 'L206']
u0 +++$+++ u2 +++$+++ m0 +++$+++ ['L207', 'L208']



- raw_script_urls.txt
    -原始来源的url( the urls from which the raw sources were retrieved)


# 斯坦福大学的培训课程，机器人的原始数据进行了编码，
