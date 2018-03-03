
<h2><a href="#思考题" aria-hidden="true" class="anchor" id="user-content-思考题"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>思考题</h2>
<ul>

<li>
<p>你理解的对于类似ucore这样需要进程/虚存/文件系统的操作系统，在硬件设计上至少需要有哪些直接的支持？至少应该提供哪些功能的特权指令？</p>
在硬件上需要时钟、CPU、内存及MMU、硬盘等外设的控制器、中断控制器等的直接支持，应该提供中断处理（允许和禁止中断，控制屏蔽位）、进程切换、写特殊寄存器、直接执行I/O操作、访存、响应时钟等功能的特权指令。

</li>

<li>
<p>你理解的x86的实模式和保护模式有什么区别？物理地址、线性地址、逻辑地址的含义分别是什么？</p>
实模式和保护模式可以访问的物理内存空间大小不同，实模式下地址位数为20位，只能访问1MB的内存空间，保护模式下地址位数为32,可以访问4GB的内存空间。物理地址是指CPU地址总线上实际的地址信号；线性地址（虚拟地址）是指逻辑地址到物理地址变换的中间层，它由基地址和段内偏移构成；逻辑地址是指有地址变换功能的计算机中访存指令中的地址立即数。
</li>

<li>
<p>理解list_entry双向链表数据结构及其4个基本操作函数和ucore中一些基于它的代码实现（此题不用填写内容）</p>

</li>

<li>
<p>对于如下的代码段，请说明":"后面的数字是什么含义</p>
":"后面的数字表示定义结构体中该成员变量所占的位数。
</li>
</ul>

<pre><code> /* Gate descriptors for interrupts and traps */
 struct gatedesc {
    unsigned gd_off_15_0 : 16;        // low 16 bits of offset in segment
    unsigned gd_ss : 16;            // segment selector
    unsigned gd_args : 5;            // # args, 0 for interrupt/trap gates
    unsigned gd_rsv1 : 3;            // reserved(should be zero I guess)
    unsigned gd_type : 4;            // type(STS_{TG,IG32,TG32})
    unsigned gd_s : 1;                // must be 0 (system)
    unsigned gd_dpl : 2;            // descriptor(meaning new) privilege level
    unsigned gd_p : 1;                // Present
    unsigned gd_off_31_16 : 16;        // high bits of offset in segment
 };
</code></pre>

<ul>
<li>对于如下的代码段，</li>
</ul>
<pre><code>#define SETGATE(gate, istrap, sel, off, dpl) {            \
    (gate).gd_off_15_0 = (uint32_t)(off) &amp; 0xffff;        \
    (gate).gd_ss = (sel);                                \
    (gate).gd_args = 0;                                    \
    (gate).gd_rsv1 = 0;                                    \
    (gate).gd_type = (istrap) ? STS_TG32 : STS_IG32;    \
    (gate).gd_s = 0;                                    \
    (gate).gd_dpl = (dpl);                                \
    (gate).gd_p = 1;                                    \
    (gate).gd_off_31_16 = (uint32_t)(off) &gt;&gt; 16;        \
}
</code></pre>
<p>如果在其他代码段中有如下语句，</p>
<pre><code>unsigned intr;
intr=8;
SETGATE(intr, 1,2,3,0);
</code></pre>
<p>请问执行上述指令后， intr的值是多少？</p>
因为x86为小端序，intr占32位，低16位为gd_off_15_0，高16位为gd_ss，故运行上述指令后，intr=0x10002


