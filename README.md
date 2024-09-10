// POST: Insuree/Create
[HttpPost]
[ValidateAntiForgeryToken]
public ActionResult Create(Insuree insuree)
{
    if (ModelState.IsValid)
    {
        // Calculate the base quote
        decimal quote = 50m; // Start with a base of $50 per month

        // Age-based quote adjustment
        int age = DateTime.Now.Year - insuree.DateOfBirth.Year;
        if (insuree.DateOfBirth > DateTime.Now.AddYears(-age)) age--;

        if (age <= 18)
        {
            quote += 100m;
        }
        else if (age >= 19 && age <= 25)
        {
            quote += 50m;
        }
        else
        {
            quote += 25m;
        }

        // Car year-based adjustment
        if (insuree.CarYear < 2000)
        {
            quote += 25m;
        }
        else if (insuree.CarYear > 2015)
        {
            quote += 25m;
        }

        // Car make and model-based adjustments
        if (insuree.CarMake.ToLower() == "porsche")
        {
            quote += 25m;

            if (insuree.CarModel.ToLower() == "911 carrera")
            {
                quote += 25m; // Additional charge for the 911 Carrera model
            }
        }

        // Add $10 for each speeding ticket
        quote += insuree.SpeedingTickets * 10m;

        // Add 25% if the user has had a DUI
        if (insuree.DUI)
        {
            quote *= 1.25m;
        }

        // Add 50% if the user has full coverage
        if (insuree.CoverageType == "Full")
        {
            quote *= 
@* Comment out or remove the quote field *@
@* <div class="form-group">
    @Html.LabelFor(model => model.Quote, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        @Html.EditorFor(model => model.Quote, new { htmlAttributes = new { @class = "form-control" } })
        @Html.ValidationMessageFor(model => model.Quote, "", new { @class = "text-danger" })
    </div>
</div> *@
// GET: Insuree/Admin
public ActionResult Admin()
{
    // Retrieve all insurees to show in the admin view
    var insurees = db.Insurees.ToList();
    return View(insurees);
}
@model IEnumerable<YourNamespace.Models.Insuree>

<h2>Admin View - All Quotes</h2>

<table class="table">
    <thead>
        <tr>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Email Address</th>
            <th>Quote</th>
        </tr>
    </thead>
    <tbody>
        @foreach (var item in Model)
        {
            <tr>
                <td>@item.FirstName</td>
                <td>@item.LastName</td>
                <td>@item.EmailAddress</td>
                <td>@item.Quote.ToString("C")</td>
            </tr>
        }
    </tbody>
</table>
git add .
git commit -m "Added quote calculation logic and admin view"
git push origin master
