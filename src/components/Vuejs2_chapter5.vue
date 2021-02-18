<template>
  <div class="container">
    <section>
      <h1>Type 2 numbers and choose operation.</h1>
      <br>
      <!-- 입력을 숫자로 파싱하기 위해 특별한 한정자인 'number' 을 사용 -->
      <input v-model.number="startNum" class="from-control">
      <select v-model="operator" class="from-control">
        <option>+</option>
        <option>-</option>
        <option>*</option>
        <option>/</option>
      </select>
      <input v-model.number="endNum" clas="from-control">
      <button type="submit" v-on:click="calculate" class="btn btn-primary">Calculate</button>    
      <h2>Result : {{startNum}} {{operator}} {{endNum}} = {{resultnum}}</h2>        
    </section>
    <br>
    <section>
      <h1>computed [버튼 클릭 없이 입력된 정보로 실시간 반영]</h1>
      <p>startNum_computed_1={{startNum_computed_1}}, endNum_computed_1={{endNum_computed}}</p>
      <p>startNum_computed_2={{startNum_computed_2}}, endNum_computed_2={{endNum_computed_2}}</p>
      <input v-model.number="startNum_computed_2">
      <br><br>
      <h1>computed 를 이용한 버튼이 없는 실시간 계산기</h1>
      <!-- 입력을 숫자로 파싱하기 위해 특별한 한정자인 'number' 을 사용 -->
      <input v-model.number="startNum_computed_new" class="from-control">
      <select v-model="operator_computed_new" class="from-control">
        <option>+</option>
        <option>-</option>
        <option>*</option>
        <option>/</option>
      </select>
      <input v-model.number="endNum_computed_new" clas="from-control">
      <h2>Result : {{startNum_computed_new}} {{operator_computed_new}} {{endNum_computed_new}} = {{resultNum_computed_new}}</h2> 
    </section>
    <br>
    <section>
      <h1>People of Value</h1>
      <ul class="list-group">
        <li v-for="(people, index) in peoples" :key="index" class="list-group-item" style="text-align:left">
          {{people.name}} {{people.votes}} <button class="btn btn-primary"  v-on:click="people.votes++" >Vote</button> 
        </li>
      </ul>
      <input @keyup.delete="clear" class="form-control" placeholder="press 'delete' to reset">
      <h2>Our mayor is {{mayor}}!</h2>      
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      startNum: 1,
      endNum: 2,
      resultnum: null,
      operator: "+",
      startNum_computed_1: 1,
      startNum_computed_2: 1,
      startNum_computed_new: 1,
      endNum_computed_new: 1,
      operator_computed_new: "+",
      peoples: [
        {name: "Mr. Black", votes: 0},
        {name: "Mr. White", votes: 0},
        {name: "Mr. Pink", votes: 0},
        {name: "Mr. Brown", votes: 0}
      ],
      clickCount: 0
    }    
  },
  methods: {
    calculate(event) {
      /*
      - event 를 받아서 아래와 같은 구문을 넣어줘야함
      - Calculate 버튼 클릭하면 페이지를 다시 로드함. 백그라운드에서 폼을 제출하고, 페이지가 다시 로드됨.
      - 폼 제출을 막기 위해 onsubmit 이벤트의 기본 동작을 취소해야함.
      */
      event.preventDefault();

      console.log(">>>>> calculate <<<<<");

      switch(this.operator) {
        case "+":
          this.resultnum = this.startNum + this.endNum
          break;
        case "-":
          this.resultnum = this.startNum - this.endNum
          break;
        case "*":
          this.resultnum = this.startNum * this.endNum
          break;
        case "/":
          this.resultnum = this.startNum / this.endNum
          break;
      }
    },
    sortValue() {
      console.log(">>>>> sortValue <<<<<");

      var testValue = this.peoples.sort(function(a,b) {
                return b.votes - a.votes;
              });

      console.log(testValue[0].name);

      return testValue[0].name;
    },
    clear: function () {
                //Turn votes of all candidate to 0 using map() function.
                console.log("clear");

                this.peoples = this.peoples.map(function (people) {
                    people.votes = 0;
                    return people;
                })
            }
  },
  computed: {
    endNum_computed: function() {
      return this.startNum_computed_1 + 1
    },
    endNum_computed_2: function() {
      // return parseFloat(this.startNum_computed_2) + 1
      return this.startNum_computed_2 + 1
    },
    resultNum_computed_new : function() {
      // switch 구문에 리턴을 넣으면 안되는듯... 왜지... 그래서 변수에 담아서 리턴해보니 처리됨...
      var result = 0;

      switch(this.operator_computed_new) {
        case "+":
          result = this.startNum_computed_new + this.endNum_computed_new
          break;
        case "-":
          result = this.startNum_computed_new - this.endNum_computed_new
          break;
        case "*":
          result = this.startNum_computed_new * this.endNum_computed_new
          break;
        case "/":
          result = this.startNum_computed_new / this.endNum_computed_new
          break;
      }

      return result;

    },
    mayor: function () {
        return this.sortValue();
    }
  }
}
</script>