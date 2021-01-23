<template>
<table class="chess-board">
  <tbody>
  <tr>
    <th></th>
    <th v-for="(_,x) in rows[0]" :key="x">{{columnLabel(x)}}</th>
  </tr>
  <tr v-for="(row, y) in rows" :key="y">
    <th>{{rowLabel(y)}}</th>
    <td v-for="(cellValue, x) in row" :key="x"
        :id="'cell:' + columnLabel(x) + rowLabel(y)"
        @click="setStartEnd(x,y)"
    >
      {{cellValue}}
    </td>
  </tr>
  </tbody>
</table>
</template>


<script>
import {reactive} from 'vue';

const rowLabel = function (y) {
  return 8 - y;
};
const columnLabel = (function() {
  const letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'];
  return x => letters[x];
}());

export default {
  name: 'Board',
  data: function(){
      return {
        selected: undefined
      }
    },
  methods: {
    displayPosition: function(x,y){
      console.log(x, y);
    },
    setStartEnd: function(x,y){
      this.displayPosition(x,y);
      if (this.selected){
        this.move(this.selected.x,this.selected.y, x,y)
        this.selected = undefined;
        return
      }
      if (this.rows[x][y]!==''){
        this.selected = {x,y};
      }
    },
    move: function(x1,y1, x2,y2){
      this.rows[y2].splice(x2, 1, this.rows[y1][x1]);
      this.rows[y1].splice(x1, 1, '');
    },
    rowLabel,
    columnLabel
  },
  computed: {
    rows: function() {
      // Ensure properly filled in, even when accepting board data as prop and it will lack the empty cells
      return [
        reactive(['♜', '♞', '♝', '♛', '♚', '♝', '♞', '♜']),
        reactive(['♟', '♟', '♟', '♟', '♟', '♟', '♟', '♟']),
        reactive(['', '', '', '', '', '', '', '']),
        reactive(['', '', '', '', '', '', '', '']),
        reactive(['', '', '', '', '', '', '', '']),
        reactive(['', '', '', '', '', '', '', '']),
        reactive(['♙', '♙', '♙', '♙', '♙', '♙', '♙', '♙']),
        reactive(['♖', '♘', '♗', '♕', '♔', '♗', '♘', '♖']),
      ];
    }
  }
}
</script>

<style scoped>
  .chess-board { border-spacing: 0; border-collapse: collapse; }
  .chess-board th { padding: .5em; }
  .chess-board th + th { border-bottom: 1px solid #000; }
  .chess-board th:first-child,
  .chess-board td:last-child { border-right: 1px solid #000; }
  .chess-board tr:last-child td { border-bottom: 1px solid; }
  .chess-board th:empty { border: none; }
  .chess-board td { width: 1.5em; height: 1.5em; text-align: center; font-size: 32px; line-height: 0;}
  /*.chess-board tr:nth-child(2n+1) td:nth-of-type(2n+1),*/
  /*.chess-board tr:nth-child(2n+2) td:nth-of-type(2n+2)*/
  .chess-board tr:nth-child(odd) td:nth-of-type(odd),
  .chess-board tr:nth-child(even) td:nth-of-type(even)
  { background: #aaa; }
  .chess-board tr:nth-child(even) td:nth-of-type(odd),
  .chess-board tr:nth-child(odd) td:nth-of-type(even)
  { background: #eee; }
</style>