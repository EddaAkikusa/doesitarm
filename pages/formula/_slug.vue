<template>
    <section class="container py-32">
        <div class="flex flex-col items-center text-center">
            <h1 class="title text-sm md:text-2xl font-semibold">
                Does <code>{{ app.name }}</code> work on Apple Silicon when installed via Homebrew?
            </h1>
            <h2 class="subtitle text-2xl md:text-5xl font-bold py-6">
                {{ app.text }}
            </h2>

            <small class="data-credit text-sm opacity-75 text-center mb-4">
                <span>According to Github</span>
            </small>

            <div
                class="comments text-sm mb-8"
                v-html="app.content"
            />

            <div class="links space-y-6 sm:space-x-6 mb-8">
                <LinkButton
                    v-for="(link, i) in app.relatedLinks"
                    :key="i"
                    :href="link.href"
                    target="_blank"
                    class=""
                >{{ (i === 0) ? 'View' : link.label }}</LinkButton>
            </div>



        </div>
    </section>
</template>

<script>
import LinkButton from '~/components/link-button.vue'
import EmailSubscribe from '~/components/email-subscribe.vue'
import ThomasCredit from '~/components/thomas-credit.vue'

import homebrewList from '~/static/homebrew-list.json'

export default {
    components: {
        LinkButton,
        EmailSubscribe,
        ThomasCredit
    },
    async asyncData ({ params: { slug } }) {

        return {
            slug,
            app: homebrewList.find(app => (app.slug === slug))
        }
    },
    head() {
        return {
            title: `Does ${this.app.name} work on Apple Silicon?`,
            // meta: [
            //     // hid is used as unique identifier. Do not use `vmid` for it as it will not work
            //     {
            //         hid: 'description',
            //         name: 'description',
            //         content: 'My custom description'
            //     }
            // ]
        }
    }
}
</script>
