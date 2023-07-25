<template>
    <img v-if="imageUrl" :src="imageUrl" :alt="`Profile picture of {{ athleteName }}`" class="avatar" />
    <div v-else :class="['avatar', 'avatarWithOnlyInitials']" :style="{backgroundColor}">{{ initials }}</div>
</template>

<script>
export default {
    name: 'Avatar',
    props: {
        athleteName: {
            required: true,
            type: String
        },
        imageUrl: String
    },
    computed: {
        backgroundColor: function () {
            if (!this.imageUrl && this.initials.length === 2) {
                const lastNameFirstLetter = this.initials.charAt(1).toLowerCase();
                if (['a', 'b', 'c', 'd'].includes(lastNameFirstLetter)) {
                    return '#f1603c';
                }
                if (['e', 'f', 'g', 'h'].includes(lastNameFirstLetter)) {
                    return '#6082fa'
                }
                if (['i', 'j', 'k', 'l'].includes(lastNameFirstLetter)) {
                    return '#827cb8'
                }
                if (['m', 'n', 'o', 'p'].includes(lastNameFirstLetter)) {
                    return '#0097a4'
                }
                if (['q', 'r', 's', 't'].includes(lastNameFirstLetter)) {
                    return '#ffe066'
                }
                return '#ffa94d'
            }
            return 'inherit';
        },
        initials: function () {
            const nameArray = this.athleteName.split(' ');

            // Make sure we have at least a first and last name
            if (nameArray.length > 1) {
                return `${nameArray[0].charAt(0).toUpperCase()}${nameArray[1].charAt(0).toUpperCase()}`
            }

            // If they don't have a correctly input name we should probably consider adding a default avatar image or otherwise handling it
            return ''
        }
    }
}
</script>

<style scoped>
.avatar {
  border-radius: 50%;
  height: 6.125rem;
  width: 6.125rem;
}

.avatarWithOnlyInitials {
    align-items: center;
    color: #FFFFFF;
    font-size: 2rem;
    display: flex;
    justify-content: center;
}
</style>