<template>
  <div>
    <form @submit="generateCeasarCipher">
      <input v-model="originalText" type="text" name="org-text" placeholder="Enter Text Here " />
      <input type="submit" value="View Ceasar Code" />
      <p>CAESAR CIPHER : '{{this.cipherText}}'</p>
    </form>
  </div>
</template>
<script>
export default {
  name: "CeasarCipher",
  data() {
    return {
      originalAlphabet: [
        "A",
        "B",
        "C",
        "D",
        "E",
        "F",
        "G",
        "H",
        "I",
        "J",
        "K",
        "L",
        "M",
        "N",
        "O",
        "P",
        "Q",
        "R",
        "S",
        "T",
        "U",
        "V",
        "W",
        "X",
        "Y",
        "Z"
      ],
      originalText: "",
      scatterdArray: [],
      cipherText:""
    };
  },
  methods: {
    generateCeasarCipher(event) {
      event.preventDefault();
      const ceasarFactor = 5;
      let newLetterIndex = 0;
      let spilittedChars = this.originalText.split("");
      let indexOfChar = 0;
      let ceasarCharArray = [];
      spilittedChars.forEach(char=>{   
          indexOfChar = this.originalAlphabet.findIndex((letter)=>{return letter == char});
          if((indexOfChar+ceasarFactor)>(this.originalAlphabet.length-1)){
              newLetterIndex = (indexOfChar+ceasarFactor)-(this.originalAlphabet.length);
          }else{
              newLetterIndex = indexOfChar+ceasarFactor;
          }
          ceasarCharArray.push(this.originalAlphabet[newLetterIndex]);
      })
      this.cipherText = ceasarCharArray.join("");
      console.log("NEW: ",ceasarCharArray.join(""));
    }
  }
};
</script>
<style scoped>
</style>