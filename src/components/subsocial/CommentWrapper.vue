<template>
  <div>
    <template v-if="!commentsVisible && !nested">
      <b-button v-if="replyCount"  type="is-primary" @click="commentsVisible = true" >{{ $t('subsocial.showComments') }} {{ replyCount }}</b-button>
      <p v-else class="title mt-2 is-6 has-text-bold">{{ $t('subsocial.noComment') }}</p>
    </template>
    <template v-else>
      <CommentAdapter v-for="(comment, i) in comments" :key="i" :comment="comment" :actionDisabled="actionDisabled" :index="i" @change="reloadComment" />
    </template>
  </div>
</template>

<script lang="ts" >
import { Component, Prop, Vue } from 'vue-property-decorator'
import { resolveSubsocialApi } from './api'
// import { PostType } from './types'
import BN from 'bn.js'

const components = {
  CommentAdapter: () => import('./CommentAdapter.vue')
}

@Component({
  name: 'CommentWrapper',
  components
})
export default class CommentWrapper extends Vue {
  @Prop(String) public postId!: string;
  @Prop(Boolean) public nested!: boolean;
  @Prop(Boolean) public actionDisabled!: boolean;
  protected comments: unknown[] = [];
  protected commentsVisible = false;
  protected loading = false;
  protected replyCount = 0;

  public async mounted() {
    // const ss = await resolveSubsocialApi()

    // if (this.postId) {
    //   if (!this.nested) {
    //     this.replyCount = (await ss.findPublicPost(new BN(this.postId)))?.struct.replies_count.toNumber() || 0
    //   }
    //   const commentIds = await ss.substrate.getReplyIdsByPostId(new BN(this.postId))
    //   const commentPromises =  commentIds.map(cm => ss.findPublicPost(cm))
    //   this.comments = await Promise.all(commentPromises)

    // }

  }

  protected async reloadComment(index: number) {
    // const commentId = this.comments[index]?.struct.id
    // const ss = await resolveSubsocialApi()
    // const comment = await ss.findPublicPost(commentId as any)
    // console.log('Updated comment', comment)
    // this.$set(this.comments, index, comment)
  }
}
</script>
