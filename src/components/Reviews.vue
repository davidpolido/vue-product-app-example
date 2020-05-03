<template>
  <div class="review-container">
    <div class="reviews">
      <h4>Reviews</h4>
      <p v-if="!reviews.length">There are no reviews yet!</p>
      <ul v-else>
        <li v-for="(review, index) in reviews" :key="index">
          <p>{{ review.name }} ({{ review.rating }} star(s))</p>
          <p>{{ review.review }}</p>
        </li>
      </ul>
    </div>

    <div class="make-review">
      <h4>Make a Review</h4>
      <form class="review-form" @submit.prevent="onSubmit">
        <p v-if="errors.length">Please correct the following error(s):</p>
        <ul>
          <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
        </ul>
        <p>
          <label for="name">Name:</label>
          <input id="name" v-model="name" />
        </p>
        <p>
          <label for="review">Review:</label>
          <textarea id="review" v-model="review"></textarea>
        </p>
        <p class="rating-container">
          <label for="rating">Rating:</label>
          <select id="rating" v-model.number="rating">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
          </select>
        </p>
        <p class="submit-container">
          <input class="submit-btn" type="submit" value="Submit" />
        </p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: null,
      review: null,
      rating: null,
      errors: [],
      tabs: ["Reviews", "Make a Review"],
      selectedTab: "Reviews",
      reviews: []
    };
  },
  methods: {
    onSubmit() {
      if (this.name && this.review && this.rating) {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating
        };

        this.reviews.push(productReview);
        // this.$emit("review-submitted", productReview);

        this.name = null;
        this.rating = null;
        this.review = null;
      } else {
        if (!this.name) this.errors.push("Name is required!");
        if (!this.review) this.errors.push("Review is required!");
        if (!this.rating) this.errors.push("Rating is required!");
      }
    }
  }
};
</script>

<style scoped>
.review-container {
  margin-top: 40px;
  flex-basis: 100%;
  display: flex;
  justify-content: space-between;
  padding: 20px;
}

.reviews {
  flex-grow: 3;
}

.make-review {
  width: 40%;
}

.review-form {
  padding: 20px;
  padding-bottom: 5px;
  border: 1px solid #d8d8d8;
  border-radius: 1em;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}
#name {
  border-radius: 1em;
  border: 1px solid #d4d4d4;
}

#rating {
  width: 80px;
  display: block;
}

textarea {
  width: 100%;
  height: 60px;
  border-radius: 1em;
  border: 1px solid #d4d4d4;
}

.submit-container {
  margin-top: 40px;
  display: flex;
  justify-content: flex-end;
}

.submit-btn {
  border: none;
  background-color: #4d5b64;
  padding: 5px;
  color: white;
  height: 50px;
  width: 90px;
  font-size: 14px;
  margin: 0px;
  border-radius: 1em;
}
</style>
