<script setup lang="ts">
import { Button } from "@/components/ui/button";
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import { format } from "date-fns";
import { ref } from "vue";
import { CalendarIcon } from "@radix-icons/vue";

import { cn } from "@/lib/utils";
import { Calendar } from "@/components/ui/calendar";
import {
  Popover,
  PopoverContent,
  PopoverTrigger,
} from "@/components/ui/popover";

const date = ref<Date>();

const id = ref(1);
const {
  data: product,
  pending,
  error,
} = await useFetch(() => `https://dummyjson.com/products/${id.value}`);
</script>

<template>
  <div class="container z-10 flex items-center justify-center pt-8">
    <div class="mt-5">
      <div class="pt-8 font-bold">សម្រាប់ រៀនធ្វើ Server Side Render</div>
      <div class="mt-5 w-[500px]">
        <Card>
          <CardHeader>
            <CardTitle>{{ product.title }}</CardTitle>
            <CardDescription>{{ product.description }}</CardDescription>
          </CardHeader>
          <CardContent>
            <div class="flex justify-center w-full">
              <Carousel
                class="relative w-full max-w-xs"
                :opts="{
                  align: 'start',
                }"
              >
                <CarouselContent>
                  <CarouselItem
                    v-for="(image, index) in product.images"
                    :key="index"
                    class="md:basis-1/2 lg:basis-1/3"
                  >
                    <div class="p-1">
                      <Card>
                        <CardContent
                          class="flex items-center justify-center p-1 aspect-square"
                        >
                          <img
                            :src="image"
                            alt=""
                            class="w-auto h-full rounded-lg"
                          />
                        </CardContent>
                      </Card>
                    </div>
                  </CarouselItem>
                </CarouselContent>
                <CarouselPrevious />
                <CarouselNext />
              </Carousel>
            </div>
          </CardContent>
        </Card>
      </div>
    </div>
    <!-- <Tabs default-value="account" class="w-[400px]">
      <TabsList class="grid w-full grid-cols-2">
        <TabsTrigger value="account"> Account </TabsTrigger>
        <TabsTrigger value="password"> Password </TabsTrigger>
      </TabsList>
      <TabsContent value="account">
        <Card>
          <CardHeader>
            <CardTitle>Account</CardTitle>
            <CardDescription>
              Make changes to your account here. Click save when you're done.
            </CardDescription>
            <Popover>
              <PopoverTrigger as-child>
                <Button
                  :variant="'outline'"
                  :class="
                    cn(
                      'w-[280px] justify-start text-left font-normal',
                      !date && 'text-muted-foreground'
                    )
                  "
                >
                  <CalendarIcon class="w-4 h-4 mr-2" />
                  <span>{{ date ? format(date, "PPP") : "Pick a date" }}</span>
                </Button>
              </PopoverTrigger>
              <PopoverContent class="w-auto p-0">
                <Calendar v-model="date" />
              </PopoverContent>
            </Popover>
          </CardHeader>
          <CardContent class="space-y-2">
            <div class="space-y-1">
              <Label for="name">Name</Label>
              <Input id="name" default-value="Pedro Duarte" />
            </div>
            <div class="space-y-1">
              <Label for="username">Username</Label>
              <Input id="username" default-value="@peduarte" />
            </div>
          </CardContent>
          <CardFooter>
            <Button>Save changes</Button>
          </CardFooter>
        </Card>
      </TabsContent>
      <TabsContent value="password">
        <Card>
          <CardHeader>
            <CardTitle>Password</CardTitle>
            <CardDescription>
              Change your password here. After saving, you'll be logged out.
            </CardDescription>
          </CardHeader>
          <CardContent class="space-y-2">
            <div class="space-y-1">
              <Label for="current">Current password</Label>
              <Input id="current" type="password" />
            </div>
            <div class="space-y-1">
              <Label for="new">New password</Label>
              <Input id="new" type="password" />
            </div>
          </CardContent>
          <CardFooter>
            <Button>Save password</Button>
          </CardFooter>
        </Card>
      </TabsContent>
    </Tabs> -->
  </div>
</template>
