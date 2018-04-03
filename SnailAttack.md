# The Golem "Snail Attack"

One thing beforehand, those of you who love me, can give me some tasty BTC: 1Dqy8z86VA28Qp133UjZZNAJN1XXwzx4bw

Today is another day where I have been enjoying the sun, a caipirinha in one hand and a havanna in the other. Yet again I have been scrolling through the golem source code, not suspecting anything evil, until I saw IT right before my eyes; another fundamental design issue, much more devastating than the rendering-verification bug I have outlined here [https://github.com/supercomputers/security_audits/blob/master/GolemKanbanana.md]().

## Some Background

Well, the problem (which was also part of the former episode) with arbitrary task execution the way golem does it, is that the processes are third party applications (such as Blender or LuxRenderer) and act as a black box.

While projects like Elastic for example have tackled this problem by introducing a special programming language (which, upon parsing, allows to tell exactly how many CPU instructions a program will need to execute in order to allow for the estimation of the runtime), there is no way to decide beforehand whether a rendering task is particularily easy or hard to render. The only way to find out how long a blender task will execute is by actually running it.

Let me point that out once again, this is important:

- When a Task comes in through the Elastic blockchain, the core client quickly assesses the so called worst case execution time and knows whether a program is particularily difficult to solve or whether it is eazy going. The programming language is designed in a way that you can assess the program's complexity before actually executing it; meaning, nodes can drop if programs are too hard to solve and they can charge a higher amount for executing it.

- When a Task come in through the Golem blockchain, as of now, the software only knows the file size of the task as well as the desired output file configuration. It does not know the complexity of the file to be rendered nor can it assess how long it will take to render.

## The Snail Attack

Well, while this little issue is not an issue at all if you rent a AWS instance, it becomes an issue (or a cool advandate, depending whether you are a worker or buyer) in a decentralized setting where other people pay money for you to carry out the rendering work.

Since there is no way to know how long a task will take, you as a buyer can only configure a maximum deadline (say, I want my task done in 10 hours and not later) and a desired amount you are willing to spend *PER HOUR*.

And here, the Snail Attack kicks in. Once you have secured a task for yourself, you have no incentive to carry out the work fast. In fact, since the golem node has no way of knowing whether you are actually still working on the job because it is so complex or if you are just stalling, you can turn full snail and render as slow as you can: just use the entire time you have until the deadline time.

This is problematic is many ways. First, of course, the incentive is not to work as fast as you can but in fact as slow as you can. As long as you deliver before the deadline, you are fine and you get paid. Unforunately for the seller, he ends up paying you a lot more than he should. For example, he pays your caipirinha that you are enyoing in the time you are witholding the task result for another few hours before you disclose it.

## Verdict

If this problem is not solved, people will be paying the full timeout period because the incentive clearly is to work as slow as possible. Probably, there will be a rush on tasks to secure as many as possible, and locking them for the full timeout deadline period for maximum profit. This needs to be solved (if it can be solved at all).
