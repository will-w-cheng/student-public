<style>
  body {
    background-color: #171515;
    color: #00ffcc; 
    animation: fadeInAnimation ease 3s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }
  .typewriter h1 {
    position: relative; /* For cursor positioning */
    font-family: Monospace;
    white-space: nowrap;
    margin: 0 auto;
    letter-spacing: 0.015em;
    color: #0099cc; 
    overflow: hidden;
  }

  .typewriter h1::after {
    content: '';
    position: absolute;
    bottom: 0;
    right: -0.015em; /* Adjust to align the cursor with text */
    border-right: .015em solid orange;
    height: 1.2em; /* Adjust to match font size */
    animation: blink-caret .75s step-end infinite;
  }

  h2 {
    color: #0099cc;
  }

  @keyframes typing {
    from { width: 0 }
    to { width: 100% }
  }

  @keyframes deleting {
    from { width: 100% }
    to { width: 0 }
  }

  @keyframes continuousTypingDeleting {
    0%, 100% {
      width: 0;
      visibility: hidden;
    }
    50% {
      width: 100%;
      visibility: visible;
    }
  }

  /* Slower blinking animation */
  @keyframes blink-caret {
    from, to {
      opacity: 0;
    }
    25%, 75% {
      opacity: 1;
    }
  }
</style>


<div class="typewriter">
  <h1>Prilasey's Page</h1>
</div>

<!-- Rest of your content -->

<script>
  const typewriter = document.querySelector('.typewriter h1');
  typewriter.style.animation = 'continuousTypingDeleting 8s infinite'; // Adjust the duration as needed
</script>

Go to my [Github account](https://github.com/will-w-cheng) 😈😈😈😈😈😈😈😈😈😈😈😈😈, please star all my repos!!


<iframe width="560" height="315" src="https://www.youtube.com/embed/K63R4vMwlDY" frameborder="0" allowfullscreen></iframe>



## Overview of Hacks, Study and Tangibles.
Blogging in GitHub pages is a way to learn and code at the same time!

![csse](/student/images/image.jpg)






- 👋Hi my name is <span style="color: blue;">Will Cheng</span>
- 👀 I’m interested in Cybersecurity (CyberPatriot XIV National Finalist), Biodata engineering, Neuroimaging, Computer Science, Gaming, and Competitive Programming
- 🌱 I’m currently researching at [Population Neuroscience and Genetics Lab at UCSD](https://chd.ucsd.edu/research/PoNG/index.html), where I've made a VCF file parser to count mutational differences in genetic data
- 💞️ Please <span style="color: yellow;">star</span> all my github repositories, would be deeply appreciated  
- 📫 Email me @ will.wi.cheng@gmail.com
- 😄 Here's a compilation of all my favorite cat meme videos [Link](https://www.youtube.com/watch?v=D5zRI0KNQh0&ab_channel=Meowthemall) yay


## Here's a todo list of what I need to do for this class
- [x] Imporve my markdown
- [ ] Learn python
- [ ] Learn Java
- [x] Learn how to use git
- [x] Use a good theme


