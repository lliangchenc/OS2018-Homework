
<h2><a href="#第三讲-启动中断异常和系统调用-思考题" aria-hidden="true" class="anchor" id="user-content-第三讲-启动中断异常和系统调用-思考题"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>第三讲 启动、中断、异常和系统调用-思考题</h2>
<h2><a href="#31-bios" aria-hidden="true" class="anchor" id="user-content-31-bios"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>3.1 BIOS</h2>
<ul>
<li>BIOS从磁盘读入的第一个扇区是是什么内容？为什么没有直接读入操作系统内核映像？</li>
一般来说，BIOS从主引导扇区中读入bootloader，再由bootloader完成OS的加载；对于x86架构，BIOS从主引导扇区中读取主引导记录，主引导记录由启动代码和硬盘的分区表构成，启动代码再读取活动分区的引导扇区代码，再由该代码完成OS的加载。因为BIOS完成硬件初始化和自检后，文件系统还没建立，BIOS无法从硬盘
中直接读取OS，硬盘中有不同的分区，BIOS无法获取分区的信息，无法确定OS的位置、大小等信息。
<li>比较UEFI和BIOS的区别。</li>
UEFI为统一的可扩展固件接口，是一种接口标准，其目的是为所有平台提供一致的操作系统启动服务；BIOS为固化在主板上的一段程序，负责硬件的启动自检、引导程序的加载等功能。与BOIS相比，UEFI具有以下特点：通用性更强、支持的容量更大，由于MBR的限制，BIOS无法启动超过2TB的硬盘，而UEFI可以；配置更灵活，交互性更好，UEFI的Shell具有更好的交互性，可以选择启动文件、硬件驱动等；安全性更好，UEFI的启动需要独立的分区，与其余硬盘分区隔离，不易被破坏。

</ul>
<h2><a href="#32-系统启动流程" aria-hidden="true" class="anchor" id="user-content-32-系统启动流程"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>3.2 系统启动流程</h2>
<ul>
<li>分区引导扇区的结束标志是什么？</li>
结束的标志为0x55AA。
<li>在UEFI中的可信启动有什么作用？</li>
通过启动的数字签名检查保证操作的安全性。
</ul>
<h2><a href="#33-中断异常和系统调用比较" aria-hidden="true" class="anchor" id="user-content-33-中断异常和系统调用比较"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>3.3 中断、异常和系统调用比较</h2>
<ul>
<li>什么是中断、异常和系统调用？</li>
中断是对指外设（时钟、键盘等）发出的信号的响应；异常是指对程序执行过程中出现的异常行为的响应；系统调用是指对系统调用指令的响应。
<li>中断、异常和系统调用的处理流程有什么异同？</li>
从源头看，中断的的源头是外设，异常和系统调用的源头是应用程序；从响应方式看，中断是异步的，异常是同步的，系统调用则两者均有可能；从处理机制看，中断的处理对用户是透明的，异常会重新杀死应用程序或重新执行当前指令，系统调用会等待或继续执行下一条指令。
<li>以ucore lab8的answer为例，uCore的系统调用有哪些？大致的功能分类有哪些？</li>
</ul>
<h2><a href="#34-linux系统调用分析" aria-hidden="true" class="anchor" id="user-content-34-linux系统调用分析"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>3.4 linux系统调用分析</h2>
<ul>
<li>通过分析<a href="https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex0.md">lab1_ex0</a>了解Linux应用的系统调用编写和含义。(仅实践，不用回答)</li>
<li>通过调试<a href="https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex1.md">lab1_ex1</a>了解Linux应用的系统调用执行过程。(仅实践，不用回答)</li>
</ul>
<h2><a href="#35-ucore系统调用分析-扩展练习可选" aria-hidden="true" class="anchor" id="user-content-35-ucore系统调用分析-扩展练习可选"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>3.5 ucore系统调用分析 （扩展练习，可选）</h2>
<ul>
<li>基于实验八的代码分析ucore的系统调用实现，说明指定系统调用的参数和返回值的传递方式和存放位置信息，以及内核中的系统调用功能实现函数。</li>
<li>以ucore lab8的answer为例，分析ucore 应用的系统调用编写和含义。</li>
<li>以ucore lab8的answer为例，尝试修改并运行ucore OS kernel代码，使其具有类似Linux应用工具<code>strace</code>的功能，即能够显示出应用程序发出的系统调用，从而可以分析ucore应用的系统调用执行过程。</li>
</ul>
<h2><a href="#36-请分析函数调用和系统调用的区别" aria-hidden="true" class="anchor" id="user-content-36-请分析函数调用和系统调用的区别"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>3.6 请分析函数调用和系统调用的区别</h2>
<ul>
<li>系统调用与函数调用的区别是什么？</li>
指令的特权级不同、指令的功能不同、系统调用需要切换堆栈。
<li>通过分析<code>int</code>、<code>iret</code>、<code>call</code>和<code>ret</code>的指令准确功能和调用代码，比较函数调用与系统调用的堆栈操作有什么不同？</li>
call/ret指令会维护用户态的程序运行栈，完成对应的push/pop操作，int/iret指令会修改特权级，切换到内核态堆栈，对其完成相应的操作。
</ul>
<h2><a href="#课堂实践-在课堂上根据老师安排完成课后不用做" aria-hidden="true" class="anchor" id="user-content-课堂实践-在课堂上根据老师安排完成课后不用做"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>课堂实践 （在课堂上根据老师安排完成，课后不用做）</h2>
<h3><a href="#练习一" aria-hidden="true" class="anchor" id="user-content-练习一"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>练习一</h3>
<p>通过静态代码分析，举例描述ucore键盘输入中断的响应过程。</p>
<h3><a href="#练习二" aria-hidden="true" class="anchor" id="user-content-练习二"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>练习二</h3>
<p>通过静态代码分析，举例描述ucore系统调用过程，及调用参数和返回值的传递方法。</p>


