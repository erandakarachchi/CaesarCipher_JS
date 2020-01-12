<template>
  <div>
    <link
      rel="stylesheet"
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css"
      integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh"
      crossorigin="anonymous"
    />
    <div class="header">
      <nav class="navbar navbar-light header">
        <a class="navbar-brand" href="#">Caesar Cipher</a>
      </nav>
    </div>
    <form @submit="generateCeasarCipher">
      <input
        v-model="originalText"
        type="text"
        name="org-text"
        class="form-control text-input"
        placeholder="Enter Text Here "
      />
      <input type="submit" class="btn btn-primary button-input" value="View Ceasar Code" />
      <div class="alert alert-success output-text" role="alert">Encrypted : {{this.cipherText}}</div>
       <div class="alert alert-success output-text" role="alert">Decrypted : {{this.decrypytedCipherText}}</div>
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
      cipherText: "",
      decrypytedCipherText : "",
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
      spilittedChars.forEach(char => {
        indexOfChar = this.originalAlphabet.findIndex(letter => {
          return letter == char;
        });
        if (indexOfChar + ceasarFactor > this.originalAlphabet.length - 1) {
          newLetterIndex =
            indexOfChar + ceasarFactor - this.originalAlphabet.length;
        } else {
          newLetterIndex = indexOfChar + ceasarFactor;
        }
        ceasarCharArray.push(this.originalAlphabet[newLetterIndex]);
      });
      this.cipherText = ceasarCharArray.join("");
      this.originalText = "";
      this.decryptCeasarCipher(this.cipherText,ceasarFactor);
    },
    decryptCeasarCipher(encryptedText,ceasarFactor){
      console.log(encryptedText,ceasarFactor);
      let splittedEncrptedText = encryptedText.split("");
      let indexOfChar = 0;
      let newLetterIndex = 0;
      splittedEncrptedText.forEach((char)=>{
        indexOfChar = this.originalAlphabet.findIndex(letter=>{return letter==char});
        if((indexOfChar-ceasarFactor)<0){
          newLetterIndex = ceasarFactor+indexOfChar;
        }else{
          newLetterIndex = indexOfChar-ceasarFactor;
        }
        console.log(this.originalAlphabet[newLetterIndex]);
      })
    }
  }
};
</script>
<style scoped>
.header {
  width: 100%;
  background-color: #3498db;
}
.text-input {
  height: 100px;
  width: 80% !important;
  margin-left: 10%;
  margin-right: 10%;
  margin-top: 10px;
  margin-bottom: 10px;
}
.button-input {
  height: 50px;
  width: 80% !important;
  margin-left: 10%;
  margin-right: 10%;
  margin-top: 10px;
  margin-bottom: 10px;
}
.output-text {
  height: 50px;
  width: 80% !important;
  margin-left: 10%;
  margin-right: 10%;
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>