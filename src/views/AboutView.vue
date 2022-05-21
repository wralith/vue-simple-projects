<template>
  <div class="about">
    <h4>Are you peeking to my journal?</h4>
    <p>Pss... It is not about me it is about <span>this</span> page.</p>
    <ul>
      <li>
        <div class="item">
          <input type="checkbox" checked />
          <span class="done"> Todo List </span>
          <small>21 May 2022</small>
        </div>
        <p>Maybe i should add tests?</p>
      </li>
    </ul>
  </div>
</template>

<style scoped lang="scss">
.about {
  text-align: left;
  width: 50%;
  margin: auto;
  background-color: darken($neutral-gray, 3%);
  padding: 1rem;
  border-radius: 0.7rem;

  input {
    accent-color: $primary;
  }

  p span {
    color: $primary;
  }

  .done {
    text-decoration: line-through;
    color: $primary;
  }

  @media (max-width: 720px) {
    width: 90%;
  }
}

ul {
  margin: 0.5rem;
}

li {
  border: 1px solid $neutral-gray;
  border-radius: 5px;
  padding: 1rem;
  .item {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
}
</style>
