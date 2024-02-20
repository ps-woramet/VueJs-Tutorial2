Style scoped
    ถ้าไม่มีการใส่ scoped จะเป็นแบบ global
    //เมื่อใส่ scoped ส่งผลแค่ component นี้ และ children component ด้วย โดยจะให้ความสำคัญกับ parent component ก่อน

Prop
    การส่ง ค่าจาก parent component ไป children component

Custom event
    การส่ง event จาก children component ไป parent component
    เริ่มต้นโดยการส่ง event จาก children component มาด้วยคำสั่ง emit แล้วจากนั้น parent ทำการรับค่า และนำไปใช้งานใน methods
 
Slot คล้าย component แต่ส่งค่าอะไรมาก็ได้
    ต่างจาก component ตรงที่ component ต้องส่งค่า props มาแล้วแสดง ตามชื่อ prop นั้นๆ แต่ slot จะส่งอะไรมาก็ได้ไม่ต้องระบุชื่อ prop แค่ใช้ tag ครอบ
    สามารถกำหนด slot name เพื่อกำหนดพื้นที่ ที่ต้องการแสดงได้

v-model เหมือน v-bind แต่ v-model จะเป็นการผูกค่า attribute html กับ data แบบ two way
    ex. เมื่อผูก input กับ data หาก input เปลี่ยน ค่า data ก็จะเปลี่ยนด้วย / หาก data เปลี่ยน ค่า input ก็จะเปลี่ยนด้วย

0. install project 

    npm create vite@latest

1. create component

    -src > components > NewComponent.vue

        <template>
            <div>this is new component</div>
        </template>

        <script>
            export default {
                name: 'NewComponent'
            }
        </script>

    -src > App.vue

        <script>
            import NewComponent from './components/NewComponent.vue'

            export default{
            name: "App",
            components:{
                NewComponent
            }
            }
        </script>

        <template>
        <div>
            <div>App Component</div>
                <NewComponent/>
            </div>
        </template>

2. style scoped

    ถ้าไม่มีการใส่ scoped จะเป็นแบบ global
    //เมื่อใส่ scoped ส่งผลแค่ component นี้ และ children component ด้วย โดยจะให้ความสำคัญกับ parent component ก่อน

    -src > components > NewComponent.vue

        <template>
            <div id="new">this is new component</div>
        </template>

        <script>
            export default {
                name: 'NewComponent'
            }
        </script>

        <style scoped>
            div{
                color: purple;
            }
        </style>

3. Props การส่งค่า Props (parent to children) and props validation

    -src > components > PropParent.vue

        <template>
        <div>
            {{message}}
            <PropChildren propName="this is prop1" :propSalary='salary1' />
            <PropChildren propName="this is prop2" :propSalary='salary2' />
            <PropChildren propName="this is prop3" :propSalary='salary3' />
        </div>
        
        </template>

        <script>
        import PropChildren from './PropChildren.vue'

        export default {
            name: 'PropParent',
            data(){
                return{
                    message: 'this is list data component',
                    salary1: 100,
                    salary2: 120,
                    salary3: 130,
                }
            },
            components:{
                PropChildren
            }
        }
        </script>


    -src > components > PropChildren.vue
    // มีการทำ props validation

        <template>
        <div>
            {{message}}
            {{propName}}
            {{propSalary}}
        </div>
        </template>

        <script>
        export default {
            name: 'PropChildren',
            data(){
                return{
                    message: 'ข้อมูล พนักงาน'
                }
            },
            props:["propName", "propSalary"],
            props:{
                propName:{
                    type: String,
                    required: true
                },
                propSalary:{
                    type:Number,
                    default: 1000
                }
            }
        }
        </script>

        <style scoped>
            div{
                color: red;
            }
        </style>


4. Dynamic props

    -src > components > DynamicPropParent.vue
        
        <template>
            <div id="dynamicprops">
                this is Dynamic Prop Parent
                <DynamicPropChildren :propGroupName="groupName" />
            </div>
        </template>

        <script>
        import DynamicPropChildren from './DynamicPropChildren.vue'

        export default {
            name: "DynamicPropParent",
            components:{
                DynamicPropChildren
            },
            data(){
                return{
                    groupName: [
                        {name: 'this is value1', salary: '100'},
                        {name: 'this is value2', salary: '200'},
                        {name: 'this is value3', salary: '300'},
                        {name: 'this is value4', salary: '400'},
                    ]
                }
            }
        }
        </script>

        <style scoped>
            #dynamicprops{
                border: 1px solid #000;;
            }
        </style>

    -src > components > ChildrenPropDynamic.vue

        <template>
        <div>
            this is Dynamic Children Prop
            <ul>
                <li>
                    <div v-for="(item, index) in propGroupName" :key="index">
                        -id {{index}} / name {{item.name}} / salary {{item.salary}}
                    </div>
                </li>
            </ul>
        </div>
        </template>

        <script>
        export default {
            name: 'DynamicPropChildren',
            props: ["propGroupName"]
        }
        </script>

5. custom event (children to parent) 
//เมื่อ child component ต้งการติดต่อไปหา parent component ก็จะทำการปล่อย (emit) event พร้อมส่งข้อมูลมายัง parent component

    -src > components > CustomEventParent.vue
    // จะเห็นได้ว่า มีการรอรับค่า emit จาก parent component เพื่อไปเรียก method
    // <CustomEventChildren :propGroupFruit="groupFruit" @newShowFromChildren="toggleShowFunction" @deleteFromChildren="deleteFunction" />

        <template>
            <div id="customEvent">
                this is Custom Event Parent
                <CustomEventChildren :propGroupFruit="groupFruit" @newShowFromChildren="toggleShowFunction" @deleteFromChildren="deleteFunction" />
            </div>
        </template>

        <script>
        import CustomEventChildren from './CustomEventChildren.vue'

        export default {
            name: "CustomEventParent",
            components:{
            CustomEventChildren
            },
            data(){
                return{
                    groupFruit: [
                        {id: 1, name: 'this is fruit1', price: '100',show:false},
                        {id: 2, name: 'this is fruit2', price: '200',show:false},
                        {id: 3, name: 'this is fruit3', price: '300',show:false},
                        {id: 4, name: 'this is fruit4', price: '400',show:false},
                    ]
                }
            },
            methods:{
            toggleShowFunction(idFromChildren){
                this.groupFruit = this.groupFruit.map((element) => {
                if(element.id === idFromChildren){
                    return {...element, show:!element.show}
                }
                return element
                })
            },
            deleteFunction(idFromChildren){
                this.groupFruit = this.groupFruit.filter((element) => {
                return element.id !== idFromChildren
                })
                console.log('delete function parent');
            }
            }
        }
        </script>

        <style scoped>
            #customEvent{
                border: 1px solid #000;;
            }
        </style>
    
    -src > components > CustomEventChildren.vue
    // ใช้คำสั่ง emit ที่ children เพื่อส่ง event หา parent

        <template>
        <div>
            this is Custom Event Children
            <div v-for="(item, index) in propGroupFruit" :key="index">
                <div id="container">
                    <div>{{item.name}}</div>
                    <div v-show="item.show">-id {{item.id}} / name {{item.name}} / price {{item.price}}</div>
                    <button @click="showDescription(item.id)">show detail</button>
                    <button @click="deleteData(item.id)">Delete data</button>
                </div>
            </div>
        </div>
        </template>

        <script>
        export default {
            name: 'CustomEventChildren',
            props: ["propGroupFruit"],
            methods:{
                showDescription(id){
                    console.log(id);
                    //send id to parent with emit
                    this.$emit('newShowFromChildren', id);
                },
                deleteData(id){
                    console.log(id);
                    //send id to parent with emit
                    this.$emit('deleteFromChildren', id);
                }
            }
        }   
        </script>

        <style>
            #container{
                border: solid black 1px;
                margin: 1rem;
                display: flex;
                align-items: center;
                justify-content: center;
                gap: 0.5rem;
                flex-direction: column;
                padding: 1rem;
            }
        </style>

6. Slot ต่างจาก component ตรงที่ component ต้องส่งค่า props มาแล้วแสดง ตามชื่อ prop นั้นๆ แต่ slot จะส่งอะไรมาก็ได้ไม่ต้องระบุชื่อ prop แค่ใช้ tag ครอบ

    -src > components > SlotTemplate.vue
    // สามารถกำหนดขอบเขตพื้นที่แสดงได้ว่าต้องส่งพื้นที่ header มาก่อน

        <template>
            <div id="card">
                template Slot
                <br>
                <slot name="header"></slot>
                <br>
                <slot></slot>
            </div>
        </template>

        <script>
        export default {
            name: 'SlotTemplate'
        }
        </script>

        <style>
        #card{
            border: solid red 1px;
            padding: 1rem;
            margin: 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        </style>

    -src > components > SlotParent.vue
    // ทำการส่งค่าต่างๆให้ slot template
    // มีการส่งไปให้ slot name header
    // หากไม่กำหนด slot name ก็ได้แต่จะถูกส่งไป slot default แทน

        <template>
            <div>this is slot parent</div>
            <SlotTemplate>
                <template v-slot:header>hello this country</template>
                country1 from slot parent
            </SlotTemplate>
            <SlotTemplate>
                <template v-slot:header>hi this country</template>
                country2 from slot parent
            </SlotTemplate>
            <SlotTemplate>
                <template v-slot:header>bonjour this country</template>
                country3 from slot parent
            </SlotTemplate>
        </template>

        <script>
        import SlotTemplate from './SlotTemplate.vue'

        export default {
            name: 'SlotParent',
            components:{
                SlotTemplate
            }
        }
        </script>

7. v-model การผูกค่า attribute html กับ data แบบ two way

    -src > components > Vmodel.vue

        <template>
            <div>this is v-model</div>
            <div>two way data binding</div>
            <br>
            <div class="form-control">
                {{JSON.stringify(employee)}}
                <div>
                    <label>name</label>
                    <input type="text" v-model.trim="employee.name">
                </div>
                <div>
                    <label>salary</label>
                    <input type="text" v-model="employee.salary">
                </div>
                <select v-model="employee.age">
                    <option value="20">20</option>
                    <option value="21">21</option>
                    <option value="22">22</option>
                </select>
                <div>
                    <input type="radio" value='male' v-model="employee.gender">
                    <label>male</label>
                    <input type="radio" value='female' v-model="employee.gender">
                    <label>female</label>
                </div>
                <div>
                    <input type="checkbox" value="thai" v-model="employee.skill">
                    <label>thai</label>
                    <input type="checkbox" value="english" v-model="employee.skill">
                    <label>english</label>
                </div>
            </div>
        </template>

        <script>
            export default {
                name: 'Vmodel',
                data(){
                    return{
                        employee:{
                            name:'woramet',
                            salary: 1000,
                            age: '20',
                            gender: '',
                            skill: []
                        }
                    }
                }
            }
        </script>

        <style scoped>
            .form-control{
                display: flex;
                justify-content: center;
                align-items: center;
                flex-direction: column;
                gap: 2rem;
            }
        </style>
