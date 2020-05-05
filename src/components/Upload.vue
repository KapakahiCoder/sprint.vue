<template>
  <div>
    <button @click="triggerInput">
      <input type="file" class="input" style="display: none;" @click="uploadPhoto" />
      Upload!
    </button>
  </div>
</template>

<script>
export default {
  name: "Upload",
  methods: {
    triggerInput: function() {},
    uploadPhoto: function() {}
  }
};

// export default function Upload() {
//   return (
//     <div className="file-upload">
//       <form>
//         <label for="myfile">Upload a picture!</label>
//         <input type="file" id="myfile"></input>
//         <button>Upload!</button>
//       </form>
//     </div>
//   );
// }

/*

export default function Upload() {
  const triggerInput = useRef();

  return (
    <>
      <button
        className={"navbar-header, upload"}
        onClick={() => {
          triggerInput.current.click();
        }}
      >
        <input
          ref={triggerInput}
          type="file"
          className={"input"}
          accept="image/gif, image/jpeg, image/png"
          onChange={event => {
            saveObject(event.target.files[0]);
            alert("Success! Photo has been uploaded!");
          }}
        ></input>
        Upload!
      </button>
    </>
  );
}

*/

/*
Upload
 The Upload component renders a button element for the purposes of uploading an image.

 The input element should allow users to select a an image file.

 When an image file has been selected with the input element, it should ultimately save that file in a S3 bucket.

 You should use the button element in the component to trigger a click event on the invisible input element. 
 
 Check out the Vue documentation on Event Handling for a look at how to accomplish this.
*/
</script>

<style>
</style>
