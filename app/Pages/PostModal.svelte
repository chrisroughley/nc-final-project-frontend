<script lang="typescript">
  import axios from 'axios/dist/axios';


  const { closeModal }=require("svelte-native");


  export let loggedInUser;
  export let users;
  export let feed;

  let textFromUser = '';
  let value = 0;
  let imageURL = ''

  const addUpdate = async (textFromUser): Promise<void> => {
    let post = {
      user: 'John', 
      postBody: textFromUser,
      avatar: "https://i.imgur.com/4zxIRRj.jpg",
      imageURL: imageURL
    }
    await axios.put("https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/tJgU7tw7OYIlQ88spYlt/feed", post)
    closeModal();
  }

  const sendImageURL = () => {
    imageURL = "https://www.ride25.com/wp-content/uploads/2014/03/tired-racer-ride-25.jpg";
    console.log(imageURL);
  }
</script>

<style>
  label {
    font-size: 25;
    text-align: center;
  }
  .post-background {
    background-image: url("~/Images/Timber.jpg");
    padding: 20;
  }
  .post-buttons {
    background-color: honeydew;
    border-radius: 5;
  }     
  .button {
    display: inline-block;
    background-color: white;
    color: black;
    text-align: center;
    font-size: 20px;
    border-radius: 60px;
    margin-left: 80;
    margin-right: 80;
  }
  .button-photo {
    display: inline-block;
    background-color: white;
    color: black;
    text-align: center;
    font-size: 20px;
    border-radius: 60px;
    margin-bottom: 70;
    margin-left: 80;
    margin-right: 80;
  }
  .post-update {
    background-color: rgb(208, 237, 251);
    height: 100;
    border-color: black;
    border-radius: 10px;
    text-align: center;
    margin-bottom: 70;
    margin-left: 20;
  }
</style>

<page>
  <stackLayout class="post-background" >
    <stackLayout >
      <label text="Create a post" textAlign="center" color="white" fontWeight="bold" fontSize="34"/>
      <textField hint="start typing..." height="50" class="post-update" bind:text="{textFromUser}" ></textField>
      <stackLayout  height="260" >
        <scrollView orientation="horizontal" >

          <stackLayout orientation="horizontal" >    
            <image src="https://www.ride25.com/wp-content/uploads/2014/03/tired-racer-ride-25.jpg"/>
            <stackLayout></stackLayout>
            <image src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSC7MYEGTlm5cxtWNfIAn7WJL1635u4pmmZUzZVTnHRBYT6_xHatIsqwKvpdHX1alMVKoU&usqp=CAU"/>
          </stackLayout> 
        </scrollView>
      </stackLayout>
    <stackLayout>
      <button on:tap={() => sendImageURL()} text="Select Photo" class="button-photo"/>
    </stackLayout>
    <stackLayout  flexDirection="column">
      <label text="Miles completed"  textAlign="center" />
      <slider minValue=0 maxValue=30 bind:value="{value}" />
      <label text="{Math.floor(value) }" />
      <button on:tap={() => {
          addUpdate(textFromUser)
        }} text="Submit" >
      </button>
    </stackLayout>
  </stackLayout>
</page>
