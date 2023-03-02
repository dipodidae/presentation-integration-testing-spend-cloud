---
background: /assets/images/failing-rocket.jpg
class: 'text-center'
---

# Integration testing
## On the Spend cloud

A wonderful journey to software stability

---
layout: image-right
image: /assets/images/bob.jpg
---




# Why this talk?

* Integration tests affect everyone
* We just changed our integration test software
* The testing guild needs all your help
* It's not clear who's responsible

---
layout: image-right
image: /assets/images/fishbowl.jpg
---

# Integration tests?

* <tabler-api/> An API endpoint might work but it could break the UI
* <ph-heart-break-fill/> Everything can break anything
* <material-symbols-ecg-heart/> You care about the stability of the product
* <ic-baseline-support-agent/> Support Consultants can only handle so much
* <ph-frame-corners/> Unit tests are not meaningful in the big picture

---
layout: center
---

# Playwright?

| *Playright* | *Cypress* |
|---|---|
| Easy | Not that easy |
| Proactive-frame | No proactive-frame |
| Quick | Slow |
| Runs headed in WSL | No WSL |
| Very nice DX | Always a pain |
| Versatile locator | Very crappy element selector |
| IDE integration | No IDE integration |


---

# So...
## Who's  responsible?

<v-click class="w-50">

![Everyone!](/assets/images/everyone.jpg)

</v-click>

<v-click>

<style>
  img {
    max-width: 50%;
  }
</style>

### Everyone!

</v-click>

---

# How do these pipelines work?

1. Your unit tests* will run
2. Once your unit tests are green <mdi-arrow-right/> Deploy on accept
3. Playwright will run
4. <span class="text-red-600">Red</span> <material-symbols-question-mark/> check [artifacts](https://gitlab.com/proactive-software/spend-cloud/-/pipelines/793706745/builds) and fix it
5. <span class="text-green-600">Green</span> <material-symbols-question-mark/> deploy to production

---
layout: image-right
image: /assets/images/fine.jpg
---

# Downsides
* Unit tests green <material-symbols-question-mark/><openmoji-dog-face/> Everything is fine
* It's not transparent
* Testing is not sandboxed <mdi-arrow-right/> Tests can break other tests
* We have this on our radar but we need you to be involved

---

# Typical test case

```js {1|2-10|12-18}
test('should be able to enable the cost center column', async ({ page }) => {
    //user interaction
    await page.locator('.trigger > .icon').first().click()

    await page
        .locator('#list-preferences-2 div')
        .filter({
            hasText: 'Cost center',
        })
        .click()

    //expectation
    expect(
        await page
            .getByRole('cell', { name: 'Cost center' })
            .getByText('Cost center')
            .isVisible(),
    ).toBe(true)
})
```
---

# Assertions
## Popular
```js
//element
expect(locator).toBeChecked()
expect(locator).toBeEnabled()
expect(locator).toBeVisible()
expect(locator).toContainText()
expect(locator).toHaveAttribute()
expect(locator).toHaveCount()
expect(locator).toHaveText()
expect(locator).toHaveValue()
//page
expect(page).toHaveTitle()
expect(page).toHaveURL()
expect(page).toHaveScreenshot()
```

## More


There are <a href="https://playwright.dev/docs/test-assertions">many more assertions</a>

---


# Getting started
```sh
cd ~/development/spend-cloud/ui
yarn install
yarn e2e:install
```


---
layout: center
---

# Demo
```sh
yarn e2e:generate
```
