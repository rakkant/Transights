<template>
    <article class="media">
        <figure class="media-left">
            <p class="image is-64x64">
                <img src="http://bulma.io/images/placeholders/128x128.png">
            </p>
        </figure>
        <div class="media-content">
            <div class="content">
                <p class="review-name">
                    <strong>John Smith</strong> <small>@johnsmith</small>
                    <star-rating class="staritem":star-size="10" :read-only="true" :show-rating="false" :increment="1" :rating="5"></star-rating>
                <br></p>
                <p v-if="!edit">
                    {{ comment }} <small v-if="edited">- Edited</small>
                </p>
                <textarea v-else v-model="editComment"class="textarea"> {{ comment }}</textarea>
            </div>
            <div v-if="edit">
                <span class="button is-dark" @click="saveEdit()">Save</span>
                <span class="button is-dark" @click="cancelEdit()">Cancel</span>
            </div>
        </div>
        <div class="media-right">
            <dropdown :visible="visible" :position="position" @clickOut="visible = false">
                <button class="delete link" @click="visiblePopup()"></button>
                <div class="dialog" slot="dropdown">
                    <aside class="menu"><ul class="menu-list">
                        <li><a @click="editMsg">Edit</a></li>
                        <li><a>Delete</a></li>
                    </ul></aside>
                </div>
            </dropdown>
            <!-- <button class="delete"></button> -->
        </div>
    </article>
</template>

<script>
import StarRating from 'vue-star-rating'
import dropdown from 'vue-my-dropdown';

export default {
    components: {
        StarRating,
        dropdown
    },
    data() {
        return {
            visible: false,
            position: [ "center", "bottom", "right", "top" ],
            comment: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin ornare magna eros, eu pellentesque tortor vestibulum ut. Maecenas non massa sem. Etiam finibus odio quis feugiat facilisis.',
            edit: false,
            edited: false,
            editComment: ''
        }
    },
    methods: {
        editMsg(){
            this.edit = true
            this.editComment = this.comment
            this.visiblePopup()
        },
        cancelEdit(){
            this.edit = false
        },
        visiblePopup(){
            this.visible = !this.visible
        },
        saveEdit(){
            this.edited = true
            this.edit = false
            this.comment = this.editComment
        }
    }
}
</script>

<style lang="scss" scoped>
.review-name {
    display: -webkit-box;
    .staritem {
        padding-left: 5px;
    }
}

.dialog{
  background: #eee;
  border: 1px solid #ccc;
  padding: 0;
  box-shadow: 1px 1px 6px 0 #999;
}

.menu-list {
    line-height: 1.25;
    li {
        a {
            padding: .5em .75em;
            &:hover {
                color: #000000;
            }
        }
    }
}

small {
    color: #999999;
}

</style>