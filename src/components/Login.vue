<template>
  <div class="flex items-center justify-center">
    <Card
      class="backdrop-blur-xl bg-white/5 border border-white/10 rounded-2xl p-10 shadow-2xl w-[400px] text-center"
    >
      <CardHeader>
        <CardTitle class="text-white tracking-widest text-xl">
          LOGIN IN WITH SSO
        </CardTitle>
      </CardHeader>

      <CardContent>
        <div class="flex items-center space-x-2">
          <Input
            v-model="email"
            type="email"
            placeholder="Enter your email"
            class="bg-white/10 border-white/20 text-white placeholder-gray-400"
          />

          <Button
            @click="login"
            size="icon"
            class="bg-white/20 hover:bg-white/30 text-white"
          >
            <ArrowRightIcon class="w-4 h-4" />
          </Button>
        </div>
      </CardContent>
    </Card>
  </div>
</template>

<script setup>
import { ref } from "vue"

// shadcn/ui components
import { Card, CardHeader, CardTitle, CardContent } from "@/components/ui/card"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"

// icons (lucide-react but works with vue wrapper libs too)
import { ArrowRightIcon } from "lucide-vue-next"

const email = ref("")

function login() {
  if (!email.value) {
    alert("Please enter your email")
    return
  }
  console.log("Logging in with:", email.value)
  // Add SSO integration here
}
</script>
