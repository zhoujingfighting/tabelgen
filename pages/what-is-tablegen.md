<h1>What is TableGen?</h1>

* A Domain-Specific Language (DSL) originated from the LLVM project
    *  <span>[Turing complete](https://en.wikipedia.org/wiki/Turing_completeness)</span>
    > A computational system that can **compute every Turing-computable function** is called **Turing-complete**

* Originally invented to describe the instruction table of a LLVM target.
    * Ex. The <span class="highlight">operands</span>, <span class="highlight">assembly syntax</span>, and <span class="highlight">ISel rules</span> for each instruction

* Now: Used in a wide variety of (completely) different areas inside LLVM.
    * Instruction scheduling info
    * Declaring IR attributes.
    * LLVM Option subsystem (e.g. Clang’s compiler flags).




<style>
    span {
       opacity: 0.5 
    }
    .highlight {
        color: #D2122E;
    }
  .dsl {
    position: absolute;
    right: 0;
    bottom:60%;
    width: 15; /* adjust as needed */
    border: 2px solid #333; /* add border */
    padding: 20px; /* add some padding */
    background-color: #f9f9f9; /* change background color */
    border-radius: 10px; /* round the corners */
    box-shadow: 0px 0px 10px rgba(0,0,0,0.1); /*add some shadow
    }
    blockquote {
    font-style: italic; /* make the text italic */
    color: #888; /* change text color */
    border-left: 4px solid #333; /* add a left border */
    padding-left: 10px; /* add some padding */
    margin: 10px 0; /* add some margin */
  
  }
</style>

---

<h1>A perfect tool? </h1>

* Advantages
    * Code reuse
        * `.inc` files can be used everywhere
    * Automatic code generation
        * Assembler, Disassembler, Instruction selector
    * Flexibility
        *  Various backends in LLVM
    * Easy to maintain
        * Modify `td` files to add or change some attributes


* Disadvantages

    * Not friendly to newcomers
    
    * llvm/lib/Target/ARM/ARMInstrInfo.td : 6507 lines