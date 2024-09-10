# build-a-chat-bot
This project is part of the KaggleX Fellowship Program - Cohort-4 - and aim to fine-tune Gemma to build a chatbot.
The chatbot will focus on helping people achieve a balance between personal and professional life while looking at balancing online and offline life as well.

Main structure of the chatbot:

 - Interactive self-assessment tool
 - Personalized advice
 - Goal setting
 - Recommendations
   
# Example of a prompt response BEFORE finetuning with the Databricks Dolly 15K Dataset:

Instruction:
What can I do to find a balance between personal life and work?

Response:
It's very easy for me to find a balance between personal life and work, and I have a lot of tips for you.
First of all, I think you should have enough energy to do everything. You can't work if you don't have enough energy. I think you can get enough rest. I think you should get enough sleep every day and take a nap when you feel tired. I think you need to eat healthy food and have some exercise.
I think you should have enough rest. I think you need to get up early in the morning, take a walk in the park, do yoga or go for a run. I think you should have fun and be happy.
I think you can find a balance between personal life and work.

I think you should have enough energy to do everything. You can't work if you don't have enough energy
I think you can find a balance between personal life and work.
I think you can do it.

# Example AFTER finetuning with the Databricks Dolly 15K Dataset:

Instruction:
What can I do to find a balance between personal life and work?

Response:
The key is to have a good plan and stick to it. If you want to be successful at work and in your personal life, then you need balance and to be able to prioritize the right things. It is easy to get caught up in work and lose sight of your personal life or vice versa. It is a fine line to walk, and you need to be careful not to get caught up in a rut where you lose your personal life. If your personal life is suffering, then you should consider taking some time off to relax and get back into balance.

# Next STEP: build a dataset on the specific subject to improve the responses
